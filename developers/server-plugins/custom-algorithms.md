# Custom Algorithms

Adding custom algorithms or enhanced comparison between values is quite simple using the default match engine in SanteDB. If extending the blocking algorithm, you should implement:

1. IQueryFilterExtension - Which registers your extended algorithm on the HDSI query interface
2. IIDbFilterFunction - Which converts your extended HDSI query operation to SQL

If exposing a custom algorithm for scoring, you must implement either:

1. IUnaryTransform - Which transforms a single operand into another value for subsequent analysis, or
2. IBinaryTransform - Which transforms two operands into a single result

### Implementing Custom IQueryFilterExtension

An IQueryFilter extension is responsible for exposing your filter algorithm on the HDSI query interface. For example, if we wanted to expose a custom query extension for the length of a string.

```csharp
public class StringLengthFilter : IQueryFilterExtension
{
    /// <summary>
    /// Gets the name
    /// </summary>
    public string Name => "length_difference";

    /// <summary>
    /// The extension method which is used by Linq
    /// </summary>
    public MethodInfo ExtensionMethod => typeof(ExtensionMethods).GetMethod(nameof(ExtensionMethods.LengthDifference));

    /// <summary>
    /// Compose the expression in LINQ
    /// </summary>
    public BinaryExpression Compose(Expression scope, ExpressionType comparison, Expression valueExpression, Expression[] parms)
    {
        if (parms.Length != 1) throw new ArgumentOutOfRangeException("difference requires one parameter : value=:(length_difference|other)comparator");
        return Expression.MakeBinary(comparison,
                            Expression.Call(this.ExtensionMethod, scope, parms[0]),
                            valueExpression);
    }
}
```

The primary responsibilities of an IQueryFilterExpression are:

* Reserve a name \(in this case length\_difference\) for use on the HDSI interfaces
* Compose the parsed expression into a method call and comparison in a LINQ expression tree
* Expose the method information to the LINQ composer so it may transform to/from HDSI / LINQ.

This particular filter expression uses an extension method to compose on LINQ, in this case our extension method is defined as:

```csharp
public static class ExtensionMethods
{
    /// <summary>
    /// Return difference in length
    /// </summary>
    public static int LengthDifference(this String a, String b)
    {
        return Math.Abs(a.Length - b.Length);
    }
}
```

When the HDSI query engine encounters:

```csharp
/Patient?name.component.value=:(length_difference|Steve)<2
```

Your filter expression composition method will be invoked and should result in a LINQ expression of:

```csharp
patient => patient.Names.Any(name => name.Component.Any(component => component.Value.LengthDifference("steve") < 2));
```

### Implementing Custom IDbFilterFunction

The IQueryFilterExpression is responsible for taking wire-level HTTP queries and constructing LINQ expressions. This is useful for in-memory objects, however to expose the filter expression to a database, a IDbFilterFunction from the ORM Lite library needs to be implemented.

Continuing our example above, a PostgreSQL implementation of length\_difference would be:

```csharp
public class PostgreStringLengthFilter : IDbFilterFunction
{
    /// <summary>
    /// Gets the provider name, in our case PostgreSQL
    /// </summary>
    public string Provider => "npgsql";

    /// <summary>
    /// Gets the name of the transform
    /// </summary>
    public string Name => "length_difference";

    /// <summary>
    /// Create a SQL statement 
    /// </summary>
    public SqlStatement CreateSqlStatement(SqlStatement current, string filterColumn, string[] parms, string operand, Type operandType)
    {
        // Match an operand to support less than or equal to semantics
        var match = new Regex(@"^([<>]?=?)(.*?)$").Match(operand);
        String op = match.Groups[1].Value, value = match.Groups[2].Value;
        if (String.IsNullOrEmpty(op)) op = "=";
         
        return current.Append($"ABS(LENGTH({filterColumn}) - LENGTH(?)) {op} ?", QueryBuilder.CreateParameterValue(parms[0], operandType), QueryBuilder.CreateParameterValue(value, typeof(Int32)));
    }
}
```

### Implementing Custom IDataTransform for Scoring

If we wanted to use or expose our extended algorithm to the scoring engine as a string transform, we can implement an IDataTransform interface. For example, if we wanted to allow users to configure a scoring attribute:

```markup
<attribute property="name.component.value" u="0.019" m="0.85" whenNull="nonmatch" required="true" >
      <assert op="le" value="2">
        <transform name="length_difference"/>
      </assert>     
    </attribute>
```

We would implement an IBinaryDataTransformer as :

```csharp
public class StringLengthTransform : IBinaryDataTransformer
{
    /// <summary>
    /// Gets the name of the transform
    /// </summary>
    public string Name => "length_difference";

    /// <summary>
    /// Apply the transform to a and b
    /// </summary>
    public object Apply(object a, object b, params object[] parms)
    {
        if (a is String aString && b is String bString)
            return ExtensionMethods.LengthDifference(aString, bString);
        else
            throw new ArgumentOutOfRangeException("A and B must be strings");
    }
}
```

In the configuration above, the matching engine would:

1. Extract the `name.component.value` of record A and record B
2. Resolve length\_difference to our implementation of IBinaryDataTransformer
3. Call the `Apply()` method of our transformer
4. Pass the result to the next transform or compare it with the assertion provided \(in this case the result is less than 2\).

