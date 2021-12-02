# BI Render Controls

The **org.santedb.bicore** package, when used together with the **org.santedb.uicore** package provide several controls for easily rendering BI reports.

### \<report> Directive

The report directive renders a complete report execution control. This control is a tabbed view where users can set parameters, switch views, and control the rendering of the report.

```markup
<report id="'org.myreport'" view="'chart'" 
    parameters="{ 'from-date': '2019-01-01', 'to-date': '2020-01-01' }" />
```

### \<report-view> Directive

The report view directive is used when you want to control the rendering of a specific view and either want to specify your own hard-coded parameters, or feed the report values off of your own controls.

```markup
<report-view id="'org.myreport'" view="'myview'"
     parameters="{ 'from-date': '2019-01-01', 'to-date': '2020-01-01' }" />
```
