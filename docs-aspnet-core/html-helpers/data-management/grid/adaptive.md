---
title: Adaptive Rendering
page_title: Adaptive Rendering | Kendo UI Grid HtmlHelper for ASP.NET Core
description: "Get started with the ASP.NET Core Grid by Kendo UI which provides consistency to the customer experience on any device by supporting adaptive rendering."
slug: adaptive_rendering_gridhelper_aspnetcore
position: 12
---

# Adaptive Rendering

The Kendo UI Grid for ASP.NET Core provides consistency to the customer experience on any device by supporting adaptive enhancements.

For example, when you filter or edit data on mobile, Kendo UI slides in a new screen for the user, which is a departure from the desktop-like inline and popup behaviors. For a runnable example, refer to the [demo on implementing the responsive web design in the Grid](https://demos.telerik.com/aspnet-core/grid/adaptive-rendering).

## Enabling the Responsive Web Design

To enable the adaptive rendering feature, use the [`Mobile`](https://docs.telerik.com/aspnet-core/api/Kendo.Mvc.UI.Fluent/GridBuilder#mobile) method.

    @(Html.Kendo().Grid<ProductViewModel>()
        .Name("grid")
        .Mobile()
        .HtmlAttributes(new { style = "height:450px;" })
        .DataSource(dataSource => dataSource
            .Ajax()
            .Read(read => read.Action("Products_Read", "Home"))
        )
    )

## Configuring Panes on Mobile

The Pane in which the adaptive Grid is placed does not automatically expand its height and you need to define an explicit pixel Grid height by setting the `height` option.

    @(Html.Kendo().Grid<ProductViewModel>()
        .Name("grid")
        .Mobile(MobileMode.Phone)
        .HtmlAttributes(new { style = "height:450px;" })
        .DataSource(dataSource => dataSource
            .Ajax()
            .Read(read => read.Action("Products_Read", "Home"))
        )
    )

## Resizing Columns

The column resizing feature on touch screen devices is triggered when the user holds a finger on the respective column header. When the resizing icon appears, the user can resize the column by dragging.

**Figure 1: A Grid with resizable columns on a mobile device**

![Grid Resizable Columns on Mobile](adaptive-resizing-icon.png)

## Destroying Adaptive Grids

When the Grid is in its adaptive rendering mode, it generates auxiliary markup which needs to be removed if the widget is to be [destroyed](https://docs.telerik.com/kendo-ui/intro/widget-basics/destroy) manually.

To manually destroy the Grid:

1. Call [`kendo.destroy()`](https://docs.telerik.com/kendo-ui/api/javascript/kendo/methods/destroy) over the closest `.k-pane-wrapper` ancestor which is created around the Grid widget.
1. Remove the whole `.k-pane-wrapper` element from the DOM.

## See Also

* [Responsive Columns by the Grid (Demo)](https://demos.telerik.com/aspnet-core/grid/responsive-columns)
* [Adaptive Rendering by the Grid (Demo)](https://demos.telerik.com/aspnet-core/grid/adaptive-rendering)
* [JavaScript API Reference of the Kendo UI Grid](http://docs.telerik.com/kendo-ui/api/javascript/ui/grid)
