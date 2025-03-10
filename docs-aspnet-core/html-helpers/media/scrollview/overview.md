---
title: Overview
page_title: ScrollView Overview | Telerik UI for ASP.NET Core HtmlHelpers
description: "Learn the basics when working with the Kendo UI ScrollView for ASP.NET Core (MVC 6 or ASP.NET Core MVC)."
slug: htmlhelpers_scrollview_aspnetcore
position: 1
---

# ScrollView Overview

The ScrollView displays a horizontal collection of content or image views with built-in navigation between them.

It can be scrolled through dragging, gestures, arrow click or page click or tap.

The Kendo UI ScrollView provides the following key features:
* Can be initialized with HTML only.
* Features data-source binding.
* Has a customizable template.
* Provides a built-in pager.
* Allows you to programmatically scroll to a specific page through its API methods.
* Has adjustable bounce effects and scroll velocity.
* Allows you to capture user interactions by handling the events that are triggered by the widget.

The ScrollView HtmlHelper extension is a server-side wrapper for the [Kendo UI ScrollView](https://demos.telerik.com/kendo-ui/scrollview/index) widget. For more information on the ScrollView HtmlHelper for ASP.NET MVC, refer to the [UI for ASP.NET MVC documentation](http://docs.telerik.com/aspnet-mvc/helpers/scrollview/overview).

## Initializing the ScrollView

You can initialize the ScrollView either [from HTML](#from-html) or [from a data source with a template](#from-the-data-source).

### From HTML

1. Use its `Items()` method.
1. Add HTML elements for each page as part of the content of the ScrollView items.

```
<style>
    h1 {
        margin-top: 30%;
        text-align:center;
    }
</style>
 @(Html.Kendo().ScrollView()
        .Name("scrollView")
        .ContentHeight("100%")
        .Items(x =>
        {
            x.Add().Content("<h1>One</h1>");
            x.Add().Content("<h1>Two</h1>");
            x.Add().Content("<h1>Three</h1>");
        })
        .HtmlAttributes(new { style = "height:748px; width:1022px; max-width: 100%;" })
)
```

### From the Data Source

1. Create a [Kendo UI template](https://docs.telerik.com/kendo-ui/framework/templates/overview).
1. Use the `TemplateId()` method to pass it and provide a DataSource.

Make sure that the template provides the `pageSize` of the data source. If `serverPaging` is enabled, the ScrollView will request the data in advance so it becomes available before it is required, thus improving user experience. The Kendo UI ScrollView uses virtualization when it is bound to a data source and it only has three pages at all times&mdash;the current, the previous, and the next.

```
    @(Html.Kendo().ScrollView()
         .Name("scrollView")
         .ContentHeight("100%")
         .TemplateId("employee-template")
         .DataSource(d =>
                d.Custom()
                  .Type("odata")
                  .Transport(t => t.Read(r => r.Url("https://demos.telerik.com/kendo-ui/service/Northwind.svc/Employees")))
                  .ServerPaging(true)
                  .PageSize(1))
         .HtmlAttributes(new { style = "height:600px; width:890px; max-width: 100%;" })
    )
    <script id="employee-template" type="text/x-kendo-template">
        <div class="template">
            <h1>
                <span>#:TitleOfCourtesy# #: FirstName# #: LastName# </span>
            </h1>
            <h3>Title: #: Title #</h3>
            <div class="notes"><em>#:Notes#</em></div>
            <div class="country">
                #: Country #
            </div>
        </div>
    </script>
```

The following example demonstrates how to fetch data from a Controller action.

```View
@(Html.Kendo().ScrollView()
    .Name("scrollView")
    .EnablePager(false)
    .ContentHeight("100%")
    .TemplateId("scrollview-template")
     .DataSource(dataSource => dataSource
        .Custom()
        .Type("aspnetmvc-ajax")
        .Transport(transport => transport
          .Read(read => read.Action("GetScrollViewData", "Home"))
        )
        .Schema(s => s.Data("Data").Total("Total"))
        .ServerPaging(true)
        .PageSize(1))
    .HtmlAttributes(new { style = "height:200px; width:300px" })
)

<script id="scrollview-template" type="text/x-kendo-template">
    <p style="border: 2px solid blue; color: red;">#= data.SomeField #</p>
</script>
```
```Controller
public class HomeController : Controller
{
    public ActionResult Index()
    {
        return View();
    }

    [HttpPost]
    public ActionResult GetScrollViewData([DataSourceRequest]DataSourceRequest request)
    {
        IEnumerable<MyModel> data = Enumerable.Range(1, 5).Select(x => new MyModel { SomeField = "item " + x + " from page " + request.Page });
        return Json(data.ToDataSourceResult(request));
    }
}
```
```Model
public class MyModel
{
    public string SomeField { get; set; }
}
```

If you set the `PageSize` option to a larger value, you will need to use a loop in the template.

```
<script id="scrollview-template" type="text/x-kendo-template">
    # for (var i = 0; i < data.length; i++) { #
        <p style="border: 2px solid blue; color: red;">#= data[i].SomeField #</p>
    # } #
</script>
```

## Events

For a complete example on basic ScrollView events, refer to the [demo on using the events of the ScrollView](https://demos.telerik.com/aspnet-core/scrollview/events).

## See Also

* [Basic Usage of the ScrollView HtmlHelper for ASP.NET Core (Demo)](https://demos.telerik.com/aspnet-core/scrollview/index)
* [Using the API of the ScrollView HtmlHelper for ASP.NET Core (Demo)](https://demos.telerik.com/aspnet-core/scrollview/api)
* [JavaScript API Reference of the ScrollView](http://docs.telerik.com/kendo-ui/api/javascript/ui/scrollview)
