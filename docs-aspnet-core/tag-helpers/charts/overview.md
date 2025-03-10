---
title: Overview
page_title: Chart Overview | Telerik UI for ASP.NET Core Tag Helpers
description: "Learn the basics when working with the Kendo UI Chart tag helper for ASP.NET Core (MVC 6 or ASP.NET Core MVC)."
previous_url: /aspnet-core/helpers/tag-helpers/chart
slug: taghelpers_chart_aspnetcore
position: 1
---

# Charts Tag Helper Overview

The [Kendo UI Charts](http://demos.telerik.com/aspnet-core/) use modern browser technologies to render high-quality data visualizations.

All graphics are rendered on the client by using [Scalable Vector Graphics (SVG)](https://en.wikipedia.org/wiki/Scalable_Vector_Graphics) with a fallback to [Canvas](http://www.canvasgfx.com/).

The Charts support the following series types:
* Bar and Column
* Line and Vertical Line
* Area and Vertical Area
* Bullet
* Pie and Donut
* Scatter
* Scatter Line
* Bubble
* Radar and Polar

The Charts tag helper extension is a server-side wrapper for the [Kendo UI Charts](http://demos.telerik.com/kendo-ui/area-charts/index) widget and enable you to configure the Kendo UI Chart widget in ASP.NET Core applications.

## Initializing the Chart

The following example demonstrates how to define the Chart by using the Chart tag helper.

    <kendo-chart name="chart"></kendo-chart>

## Basic Configuration

The Chart tag helper configuration options are passed as attributes of the tag. The following **tagHelper** and **razor** configurations are equivalent.

```tagHelper
<kendo-chart name="chart">
    <chart-title text="Gross domestic product growth /GDP annual %/"></title>
    <chart-legend position="ChartLegendPosition.Top"></legend>
    <series-defaults type="ChartSeriesType.Column"></series-defaults>

    <series>
        <series-item name="India" data="new double[] { 3.907, 7.943, 7.848, 9.284, 9.263, 9.801, 3.890, 8.238, 9.552, 6.855 }"></series-item>
        <series-item name="Russian Federation" data="new double[] { 4.743, 7.295, 7.175, 6.376, 8.153, 8.535, 5.247, -7.832, 4.3, 4.3 }"></series-item>
        <series-item name="Germany" data="new double[] { 0.010, -0.375, 1.161, 0.684, 3.7, 3.269, 1.083, -5.127, 3.690, 2.995 }"></series-item>
        <series-item name="World" data="new double[] { 1.988, 2.733, 3.994, 3.464, 4.001, 3.939, 1.333, -2.245, 4.339, 2.727 }"></series-item>
    </series>

    <value-axis>
        <value-axis-item>
            <labels format="{0}%"></labels>
            <line visible="false" />
        </value-axis-item>
    </value-axis>

    <category-axis>
        <category-axis-item categories='new string[] { "2002", "2003", "2004", "2005", "2006", "2007", "2008", "2009", "20010", "2011", }'>
            <labels>
                <chart-category-axis-labels-padding top="135" />
            </labels>
            <line visible="false" />
        </category-axis-item>
    </category-axis>

    <tooltip visible="true" format="{0}%" template="#= series.name #: #= value #"></tooltip>
</kendo-chart>
```
```cshtml
@(Html.Kendo().Chart()
    .Name("chart")
    .Title("Gross domestic product growth /GDP annual %/")
    .Legend(legend => legend
        .Position(ChartLegendPosition.Top)
    )
    .ChartArea(chartArea => chartArea
        .Background("transparent")
    )
    .Series(series =>
    {
        series.Column(new double[] { 3.907, 7.943, 7.848, 9.284, 9.263, 9.801, 3.890, 8.238, 9.552, 6.855 }).Name("India");
        series.Column(new double[] { 4.743, 7.295, 7.175, 6.376, 8.153, 8.535, 5.247, -7.832, 4.3, 4.3 }).Name("Russian Federation");
        series.Column(new double[] { 0.010, -0.375, 1.161, 0.684, 3.7, 3.269, 1.083, -5.127, 3.690, 2.995 }).Name("Germany");
        series.Column(new double[] { 1.988, 2.733, 3.994, 3.464, 4.001, 3.939, 1.333, -2.245, 4.339, 2.727 }).Name("World");
    })
    .CategoryAxis(axis => axis
        .Name("series-axis")
        .Line(line => line.Visible(false))
    )
    .CategoryAxis(axis => axis
        .Name("label-axis")
        .Categories("2002", "2003", "2004", "2005", "2006", "2007", "2008", "2009", "2010", "2011")
    )
    .ValueAxis(axis => axis
        .Numeric()
            .Labels(labels => labels.Format("{0}%"))

            // Move the label-axis all the way down the value axis.
            .AxisCrossingValue(0, int.MinValue)
    )
    .Tooltip(tooltip => tooltip
        .Visible(true)
        .Format("{0}%")
        .Template("#= series.name #: #= value #")
    )
)
```

## See Also

* [Kendo UI for jQuery Chart Series Types](https://docs.telerik.com/kendo-ui/controls/charts/chart-types/chart-types-compatibility)
* [Basic Usage of the Kendo UI Area Charts Tag Helper for ASP.NET Core (Demo)](https://demos.telerik.com/aspnet-core/area-charts/tag-helper)
* [JavaScript API Reference of the Kendo UI Charts](https://docs.telerik.com/kendo-ui/api/javascript/dataviz/ui/chart)
