# Indicators

{% hint style="info" %}
This page documents a feature found in SanteDB v3.0
{% endhint %}

## Introduction

SanteDB's business intelligence system allows for developers to define key performance indicators which are captured and executed on defined periods. Over time, these indicators allow data analysts to determine improvement or deterioration of a KPI over time.&#x20;

Indicators differ from a [reports.md](../../../extending-santesuite/extending-santedb/applets/business-intelligence-bi-assets/bi-asset-definitions/reports.md "mention")in that an indicator allows for more granular investigation of the change of a population or indicator score over time. Examples of indicators are:

* The number of patients who present a certain symptom compared to the total patient population
* The number of children who received a vaccination compared to the total population of children
* The number of abnormal temperature events detected in a facility as a proportion of all temperature readings

In SanteDB's BI implementation, and indicator is comprised of:

* Metadata about the indicator (such as authorship, identification, status, etc.)
* A query definition - the source of data which is used to populate the indicator
* A period definition - the recurrence of measure for the indicator (example: monthly, weekly, etc.)
* A subject definition - the person/place/organization against which the indicator is measured
* Measurements - the computed measurements for the indicator
  * Stratifiers - if the measurements are dis-aggregated (for example: by age, by gender, etc.)&#x20;

The output of an indicator is a structured result containing discrete data values for numerators, denominators, exclusions to the denominator, etc.

## Defining an Indicator

An indicator is defined by creating a new `.xml` file in the `bi/`directory of your applet. This file starts with the `BiIndicatorDefinition` element and the standard BI metadata.&#x20;

```xml
<BiIndicatorDefinition 
    xmlns="http://santedb.org/bi"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://santedb.org/bi http://santedb.org/schema/v3.0/BusinessIntelligence.xsd"
    id="id.of.my.indicator"
    name="my-indicator-name"
    label="label.to.appear.in.title">
    
    <meta>
        <authors>
            <add>My Institution or Organization</add>
        </authors>
        <annotation>
            <div xmlns="http://www.w3.org/1999/xhtml">
                <p>Some description about the purpose of the indicator</p>
            </div>
        </annotation>
        <policies>
            <demand>policy.oid.to.demand.to.run.indicator</demand>
        </policies>
        <!-- when an indicator is public it will appear on user interfaces -->
        <public>true</public>
    </meta>
    
    <!-- If the indicator is sent to another system or is known by a standardized 
         identifier, then an identifier is provided -->
     <identifier system="STANDARDIZED INDICATORS FOR DEMOLAND" value="example" />
     
   <query>
       <!-- See Below -->
   </query>
   <period>
       <!-- See Below -->
   </period>
    
   <subject><!-- See Below --></subject>
    
   <measures>
       <!-- See Below -->
   </measures>
</BiIndicatorDefinition> 
```

{% hint style="info" %}
The annotations, policies, and identifier elements defined on the indicator appear on the FHIR resource `Measure` exposed from the SanteDB server on which the indicator is installed.
{% endhint %}

## Defining a Query

An indicator must be derived form a Query. This query can be referenced from a shared query (see: [queries.md](../../../extending-santesuite/extending-santedb/applets/business-intelligence-bi-assets/bi-asset-definitions/queries.md "mention")) or can be an inline query. If your indicator shares information with a report which is generated in SnateDB, you can reference the query directly:

```xml
<query ref="#org.example.bi.queries.someReportSource" name="main" />
```

If, however, our indicator **extends** the query `org.example.bi.queries.someReportSource`we would reference this query and extend it. In the example below, we normalize `someReportSource`by preparing our stratifier columns to their display names:

```xml
<query>
    <dataSources>
        <!-- Reference the primary database rather than the warehouse -->
        <add ref="#org.santedb.bi.dataSource.main" />
    </dataSources>
    <!-- We want to reference / extend the query -->
    <with ref="#org.example.bi.queries.someReportSource" name="source" />
    <!-- 
        Any parameters that are relevant to the computation or restriction of the 
        dataset such as the subject, or period are listed here. Any parameters which 
        are used in the underlying data query can also be rendered here
    -->
    <parameters>
        <add name="date-from" ref="#org.santedb.bi.core.parameter.common.date.from"
            type="date" />
        <add name="date-to" ref="#org.santedb.bi.core.parameter.common.date.to"
            type="date" />
        <add name="facility" ref="#org.santedb.bi.core.parameter.common.facility"
            type="uuid" />
    </parameters>
    
    <!-- Just like our shared query definition, we will now define one or more
         query definitions in SQL which match the invariants -->
    <definitions>
        <add>
            <!-- This query works on POSTGRES, SQLITE, and FIREBIRD -->
            <providers>
                <invariant>npgsql</invariant>
                <invariant>sqlite</invariant>
                <invariant>fbsql</invariant>
            </providers>
            <![CDATA[
            SELECT 
                source.proposal_id,
                source.proposed_date,
                source.vaccine_event_id, 
                source.vaccine_event_date,
                source.facility_id, 
                source.patient_id,
                source.patient_age_group,
                gender_code.val AS patient_gender,
                source.product_code
            FROM 
                source -- THIS IS OUR REFERENCED DATASET
                INNER JOIN cd_name_tbl gender_code ON (source.gender = gender_code.cd_id AND gender_code.obslt_vrsn_seq_id IS NULL)
            ]]>
        </add>
    </definitions>
</query>
```

## Defining a Period

Your indicator definition should define a period (how often the indicator is computed) and a subject (the place, organization, or other entity against which the indicator is being measured).

SanteDB provides four standard period definitions:

<table><thead><tr><th width="400">Period</th><th>Frequency</th></tr></thead><tbody><tr><td><code>org.santedb.bi.core.period.yearly</code></td><td>Every year (Jan 1  - Dec 31)</td></tr><tr><td><code>org.santedb.bi.core.period.monthly</code></td><td>Every month (first of month to last day of month)</td></tr><tr><td><code>org.santedb.bi.core.period.weekly</code></td><td>Every week (monday - sunday)</td></tr><tr><td><code>org.santedb.bi.core.period.daily</code></td><td>Every day (00:00 - 23:59)</td></tr></tbody></table>

The period is defined using the `<period>` element, to reuse an existing period definition you merely need to express the parameters in your query to which the period bounds apply:

```xml
<period ref="#org.santedb.bi.core.period.monthly">
    <startParameter>from-date</startParameter>
    <endParameter>end-date</endParameter>
</period>
```

To define a custom period, you will need to define a few additional elements:

```xml
<period name="bi-weekly">
    <!-- The spec is an example date representing the beginning of a valid period -->
    <spec>2025-01-13</spec>
    <!-- The period is the frequency of repeating from the spec date -->
    <period>P14D</period>
    <!-- Parameters for our query -->
    <startParameter>from-date</startParameter>
    <endParameter>end-date</endParameter>
</period>
```

## Defining a Subject

The subject defines the objects against which the indicator is being measured. A subject is defined using the `<subject>` element:

```xml
<subject
    type="Place"
    parameter="facility">
    facility
</subject>
```

## Defining Measures

Finally, an indicator must contain one or more measure definitions. A measure definition instructs the BI layer how to compute the indicator for each of the periods and subjects identified. Each measure is contained as an `<add>`element in the `<measures>`.

```xml
<measures>
    <add id="org.example.bi.indicators.administered.bcg" name="bcg-administered">
        <!-- Metadata can be used to describe the measure -->
        <meta>
            <annotation>
                <div xmlns="http://www.w3.org/1999/xhtml">
                    <p>Administrations of BCG given at facility compared to proposed</p>
                </div>
            </annotation>
        </meta>
        
        <!-- If the indicator is known by an external system -->
        <identifier system="DEMOLAND EPI INDICATORS" value="bcg-coverage" />
        
        <!-- An indicator is computed by specific instructions applied against the query -->
        <computed-by>
            <!-- Count number of actual vaccination event ids when the product is BCG -->
            <numerator fn="count-distinct">CASE WHEN product_code = 'BCG' THEN vaccine_event_id ELSE null END</numerator>
            <!-- Count number of proposed events when the product is BCG -->
            <denominator fn="count-distinct">CASE WHEN product_code = 'BCG' THEN proposal_id ELSE null END</numerator>
        </computed-by>
        
        <!-- 
            The indicator so far will report the number of performed BCG events over number of proposed BCG events 
            
            Let's stratify by the age group 
        -->
        <stratify>
            <by name="age-group">
                <!-- Can contain metadata -->
                <meta>
                    <annotation>
                        <div xmlns="http://www.w3.org/1999/xhtml">
                            <p>By Age Group</p>
                        </div>
                    </annotation>
                </meta>
                <!-- And identifier for publication -->
                <identifier system="DEMOLAND EPI INDICATORS" value="bcg-coverage:age-group" />
                 
                <!-- The column which represents the stratification grouper -->
                <select>patient_age_group</select>
                
               <!-- Sub-stratifications, for example, by age by gender -->
               <thenBy name="gender">
                   <identifier system="DEMOLAND EPI INDICATORS" value="bcg-coverage:age-group:gender"/>
                  <select>patient_gender</select>
              </thenBy>
          </by>
      </stratify>
  </add>
</measures>
```

The example above would result in an indicator which may be represented for each facility as:

| Indicator ID          | Numerator | Denominator |
| --------------------- | --------- | ----------- |
| bcg                   | 100       | 110         |
| bcg:under\_24h        | 80        | 90          |
| bcg:over\_24h         | 20        | 20          |
| bcg:under\_24h:Male   | 45        | 50          |
| bcg:under\_24h:Female | 35        | 40          |
| bcg:over\_24h:Male    | 15        | 15          |
| bcg:over\_24h:Female  | 5         | 5           |

{% hint style="info" %}
In HL7 FHIR the indicator computation is represented by `MeasureReport` which can be computed in real time using `Measure/$evaluate-measure` specifying the `periodStart`, the `subject`and the `measure`to be performed.
{% endhint %}

