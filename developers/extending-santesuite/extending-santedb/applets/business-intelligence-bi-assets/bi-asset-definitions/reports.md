# Reports

A report definition in SanteDB's BI services framework represents an asset which is ultimately rendered to one or more output formats (like HTML, XLS, etc.).

Data sources for reports can be either a view or a query which can be referenced or inline with the report definition itself.

## Report Definition Files

Report definition files define one or more data sources (query or view), metadata (including permission), and one or more views. These views represent different ways of representing data. For example you may have a report with a tabular view and a chart view.&#x20;

```markup
<?xml version="1.0" encoding="utf-8" ?>
<BiReportDefinition xmlns="http://santedb.org/bi" id="org.santedb.bi.sample.reports.eventType" label="ui.bi.sample.reports.eventType">
  <meta>
    <authors>
      <add>SanteSuite Contributors</add>
    </authors>
    <annotation>
      <div xmlns="http://www.w3.org/1999/xhtml">
        <p>A simple report</p>
      </div>
    </annotation>
  </meta>
  <dataSources>
    <view ref="org.santedb.bi.core.view.audit.date" name="main-date"/>
  </dataSources>
  <views>
    <add id="org.santedb.bi.sample.reports.eventType.main" label="ui.bi.reports.main" name="chart">
      <div xmlns="http://www.w3.org/1999/xhtml" 
         xmlns:bi="http://santedb.org/bi/view">
         <!-- Report Content -->
           
      </div>
    </add>
  </views>
</BiReportDefinition>
```

The view contents are defined using XHTML and the content is generated using view components defined in the **http://santedb.org/bi/view** namespace.

## Report View Components

There are several built-in view components which you can use for creating your report. They are:

| Component       | Description                                                      |
| --------------- | ---------------------------------------------------------------- |
| \<bi:aggregate> | Aggregate one of the reports data sources                        |
| \<bi:locale>    | Render a localized string into the report                        |
| \<bi:repeat>    | Repeat the contents of for each row contained in the data source |
| \<bi:switch>    | Conditional rendering of report components                       |
| \<bi:value>     | Bind the contents to a particular column in the current row.     |
| \<bi:chart>     | Render a pie, line, bar, radar, donut or combination chart.      |

### Aggregate Component

The aggregate component is used to aggregate a particular data source. This is useful for showing totals, averages, counts, etc.

```markup
<bi:aggregate source="dataSourceName"
     fn="aggregationFunction"
     format="numberFormat">fieldOrExpression</bi:aggregate>
```

The aggregation functions currently supported are:

| Function       | Description                                                  |
| -------------- | ------------------------------------------------------------ |
| sum            | Adds the particular field or expression together             |
| count          | Counts the number of non-null values                         |
| count-distinct | Counts the unique instances of a value or expression         |
| min            | The minimum value for the value or expression in the dataset |
| max            | The maximum value                                            |
| avg            | Average value                                                |

You can either aggregate a field, or an expression, for exam

```markup
<tfoot>
    <tr>
        <th><bi:locale>ui.total</bi:locale></th>
        <td><bi:aggregate source="main" fn="sum" format="#,###">n_patients</bi:aggregate>
    </tr>
    <tr>
        <th><bi:locale>ui.somecalc</bi:locale></th>
        <td><bi:aggregate source="main" fn="avg" format="#,###">n_patients / cohort</bi:aggregate>
</tfoot>
```

### Locale Component

The locale component will replace the value of the element with the correct string from the current locale.

```markup
<bi:locale>ui.welcome</bi:locale>
```

### Repeat Component

The repeat component is an iterator which opens a dataset and repeats until the rows in the data source are exhausted.

```markup
<bi:repeat source="dataSourceName"> 
    <!-- HTML HERE -->
</bi:repeat>
```

The contents of the repeat element is any content, for example, this component is used to create tables:

```markup
<table border="1">
    <thead>
        <tr><bi:locale>ui.date</bi:locale></tr>
        <tr><bi:locale>ui.name</bi:locale></tr>
    </thead>
    <tbody>
        <bi:repeat source="main">
            <tr>
                <td><bi:value>date</bi:value></td>
                <td><bi:value>name</bi:value></td>
            </tr>
        </bi:repeat>
    </tbody>
    <tfoot>
        <tr>
            <th>Total Patients</th>
            <th><bi:aggregate fn="count" source="main">name</bi:aggregate>
        </tr>
    </tfoot>
</table>
```

### Switch Component

The switch component is used to provide conditional rendering of components.

```markup
<bi:switch value="valueOrExpression">
    <bi:when op="eq|lt|lte|gt|gte" value="valueOrExpression" not="true|false">
        <!-- HTML HERE -->
    </bi:when>
    <bi:default>
        <!-- HTML HERE -->
    </bi:default>
</bi:switch>
```

For example, the switch statement can be used to provide iconography:

```markup
<bi:switch value="this_month">
    <bi:when op="lt" value="last_month">
        <i class="fas fa-arrow-down"></i>
    </bi:when>
    <bi:when op="gt" value="last_month">
        <i class="fas fa-arrow-up"></i>
    </bi:when>
    <bi:default>
        <i class="fas fa-equals"></i>
    </bi:default>
</bi:switch>
```

### Value Component

The value component allows the rendering of report data elements or expressions.

```markup
<bi:value when="[changed]" format="formatString">expressionOrField</bi:value>
```

The when changed indicates that the value should only be emitted when the previous rows' value is not equal to this row's value. For example:

```markup
<table>
    <thead>
        <tr>
            <th><bi:locale>ui.patient</bi:locale></th>
            <th><bi:locale>ui.visitDate</bi:locale></th>
        </tr>
    </thead>
    <tbody>
        <bi:repeat source="patientVisits">
            <tr>
                <td><bi:value when="changed">name</bi:value></td>
                <td><bi:value format="yyyy-MM-dd">visitDate</bi:value>
            </tr>
        </bi:repeat>
    </tbody>
    <tfoot>
        <tr>
            <td><bi:aggregate fn="count-distinct">name</bi:aggregate> <bi:locale>ui.patients.total</bi:locale></td>
            <td><bi:aggregate fn="count">visitDate</bi:aggregate></td>            
        </tr>
    </tfoot>
</table>
```

This may output a table such as:

| ui.patient          | ui.visitDate |
| ------------------- | ------------ |
| SMITH, JOHN         | 2019-03-11   |
|                     | 2019-04-11   |
| JONES, JENNIFER     | 2019-11-01   |
| 2 ui.patients.total | 3            |

### Chart Component

The charting component allows for quick creation of basic charts using the data found in the data source.&#x20;

```markup
<bi:chart type="pie|line|radar|donut|bar" source="dataSourceName">
    <bi:title>title of chart</bi:title>
    <bi:labels data="categoryField" format="formatString"/>
    <!-- Axis Series (allows multiple) -->
    <bi:axis type="linear|time" data="categoryOrField" label="label" format="formatString"/>
    <!-- One or more datasets -->
    <bi:dataset label="datasetLabel" backgroundColor="rgba()" 
        borderColor="rgba()" type="bar|line" fill="true|false" 
        aggregate="count|sum|avg|min|max|first|last">fieldOrExpression</bi:dataset>
</bi:chart>
```

For example, to create a simple pie chart:

```markup
<bi:chart type="pie" source="main">
    <bi:title>Patients By Gender</bi:title>
    <bi:labels data="gender"/>
    <bi:dataset label="# of Patients" fill="true" aggregate="sum">id</bi:dataset>
</bi:chart>
```

It is also possible to create composite charts

```markup
<bi:chart source="main" type="bar">
    <bi:title>Patient Trends<bi:title>
    <bi:axis type="time" data="date" format="yyyy-MM" label="Month"/>
    <bi:dataset label="Males" aggregate="sum" fill="true" 
        backgroundColor="rgba(0,0,255,0.5)">gender == 'M' ? 1 : 0</bi:dataset>
    <bi:dataset label="Females" aggregate="sum" fill="true"
        backgroundColor="rgba(0,255,0,0.5)">gender == 'F' ? 1 : 0</bi:dataset>
</bi:chart>
```

#### Reference Data / Layers

Within a bar, line or radar chart you can add reference data sets which are useful for comparing data against a known good value set. These reference sets will appear as other datasets on the chart, however are drawn from a different data source than the primary view.

Reference data sets must:

* Have their first column match the `<labels>` or `<axis>` elements as they appear on the chart
* Should be sorted in the same manner as the primary axis or dataset

Reference datasets are included via the `@ref-source` attribute on the `<bi:chart` element, and individual lines created using `<bi:refset`. For example, if there is a chart with ages, and a target population to serve as a reference set:

```xml
<bi:chart source="patient_population" type="line" ref-source="ref-targetpop">
    <bi:title>Patient Population (Age in Years)</bi:title>
    <bi:labels format="#0">(DateTime.Now - birth_time).TotalDays / 365.25</bi:labels>
    <bi:refset label="Target Population (Male)" fill="false">Male</bi:refset>
    <bi:refset label="Target Population (Female)" fill="false">Female</bi:refset>
    <bi:dataset label="Male" fn="sum">Male</bi:dataset>
    <bi:dataset label="Female" fn="sum">Female</bi:dataset>
</bi:chart>
```

#### Styling Chart Data

Charts can be styled using the following attributes on the `<bi:dataset` or `<bi:refset` as documented below.

<table><thead><tr><th>Attribute</th><th width="164">Type</th><th>Description</th></tr></thead><tbody><tr><td>backgroundColor</td><td>Color</td><td>Controls the fill color of the series</td></tr><tr><td>borderColor</td><td>Color</td><td>Controls the line color of the border</td></tr><tr><td>borderWidth</td><td>Number</td><td>Controls the width of the border drawn</td></tr><tr><td>fill</td><td>Boolean</td><td>When <code>false</code> the series will not be a filled series</td></tr><tr><td>order</td><td>Number</td><td>The relative order of the series in the chart</td></tr><tr><td>pointRadius</td><td>Number</td><td>The radius of the data points on the series (so users can see the data value)</td></tr><tr><td>spanGaps</td><td>Boolean</td><td>When true, any gaps in data will be filled, when false the line will be broken</td></tr><tr><td>barThickness</td><td>Number</td><td>When using a bar graph, controls the width of each bar.</td></tr><tr><td>skipNull</td><td>Boolean</td><td>When true, elements with no value are skipped in the dataset.</td></tr></tbody></table>
