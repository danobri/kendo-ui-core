---
title: Overview
page_title: MultiSelect Overview | Telerik UI for ASP.NET Core HtmlHelpers
description: "Learn the basics when working with the Kendo UI MultiSelect HtmlHelper for ASP.NET Core (MVC 6 or ASP.NET Core MVC)."
previous_url: /aspnet-core/helpers/html-helpers/multiselect
slug: htmlhelpers_multiselect_aspnetcore
position: 1
---

# MultiSelect HtmlHelper Overview

The [MultiSelect](http://docs.telerik.com/kendo-ui/controls/editors/multiselect/overview) displays a list of options and allows multiple selections from this list.

The widget represents a richer version of the `<select>` element and provides support for local and remote data binding, item and tag templates, and configurable options for controlling the list behavior.

The MultiSelect HtmlHelper extension is a server-side wrapper for the [Kendo UI MultiSelect](http://demos.telerik.com/kendo-ui/multiselect/index) widget. For more information on the MultiSelect HtmlHelper for ASP.NET MVC, refer to the [UI for ASP.NET MVC documentation](https://docs.telerik.com/aspnet-mvc/helpers/multiselect/overview).

## Initializing the MultiSelect

The following example demonstrates how to define the MultiSelect by using the MultiSelect HtmlHelper.

```Razor
    @(Html.Kendo().MultiSelect()
        .Name("multiselect")
        .DataTextField("ProductName")
        .DataValueField("ProductID")
        .Value(new[] { 2, 7 })
        .DataSource(source =>
        {
            source.Read(read =>
            {
                read.Action("Products_Read", "Home");
            })
            .ServerFiltering(true);
        })
    )
```
```Controller
    public class MultiSelectController : Controller
    {
        public IActionResult Index()
        {
            return View();
        }

        public JsonResult Products_Read(string text)
        {
            var result = GetProducts();

            if (!string.IsNullOrEmpty(text))
            {
                result = result.Where(p => p.ProductName.Contains(text)).ToList();
            }

            return Json(result);
        }

        private static IEnumerable<ProductViewModel> GetProducts()
        {
            var result = Enumerable.Range(0, 50).Select(i => new ProductViewModel
            {
                ProductID = "" + i,
                ProductName = "Product " + i
            });

            return result;
        }
    }
```

## Basic Configuration

The following example demonstrates the basic configuration of the MultiSelect HtmlHelper. To get a reference to an existing Kendo UI MultiSelect instance, use the [`jQuery.data()`](http://api.jquery.com/jQuery.data/) configuration option. Once a reference is established, use the [MultiSelect API](http://docs.telerik.com/kendo-ui/api/javascript/ui/multiselect#methods) to control its behavior.

```
@(Html.Kendo().MultiSelect()
    .Name("multiselect")
    .DataTextField("ProductName")
    .DataValueField("ProductID")
    .Placeholder("Select product...")
    .ItemTemplate("<span class=\"product-id-id\">#= ProductID #</span> #= ProductName #")
    .Value(new[] { 2, 7 })
    .Height(520)
    .TagMode(MultiSelectTagMode.Single)
    .DataSource(source =>
    {
        source.Read(read =>
        {
            read.Action("Products_Read", "Home");
        })
        .ServerFiltering(true);
    })
    .Events(events => events
        .Change("onChange")
        .Select("onSelect")
        .Deselect("onDeselect")
        .Open("onOpen")
        .Close("onClose")
        .DataBound("onDataBound")
        .Filtering("onFiltering")
    )
)

<script type="text/javascript">
    $(function () {
        // The Name() of the MultiSelect is used to get its client-side instance.
        var multiselect = $("#multiselect").data("kendoMultiSelect");
    });
</script>
```

## Functionality and Features

* [Binding]({% slug htmlhelpers_multiselect_databinding_aspnetcore %})
* [Grouping]({% slug htmlhelpers_multiselect_grouping_aspnetcore %})
* [Virtualization]({% slug htmlhelpers_multiselect_virtualization_aspnetcore %})
* [Templates]({% slug htmlhelpers_multiselect_templates_aspnetcore %})

## Events

You can subscribe to all MultiSelect [events](http://docs.telerik.com/kendo-ui/api/javascript/ui/multiselect#events). For a complete example on basic MultiSelect events, refer to the [demo on using the events of the MultiSelect](https://demos.telerik.com/aspnet-core/multiselect/events).

### Handling by Handler Name

The following example demonstrates how to subscribe to events by a handler name.

    @(Html.Kendo().MultiSelect()
        .Name("multiselect")
        .BindTo(new string[] { "Item1", "Item2", "Item3" })
        .Events(e => e
            .Select("multiselect_select")
            .Change("multiselect_change")
        )
    )
    <script>
        function multiselect_select() {
            // Handle the select event.
        }

        function multiselect_change() {
            // Handle the change event.
        }
    </script>


### Handling by Template Delegate

The following example demonstrates how to subscribe to events by a template delegate.

    @(Html.Kendo().MultiSelect()
        .Name("multiselect")
        .BindTo(new string[] { "Item1", "Item2", "Item3" })
        .Events(e => e
            .Select(@<text>
                function() {
                    // Handle the select event inline.
                }
            </text>)
            .Change(@<text>
                function() {
                    // Handle the change event inline.
                }
            </text>)
        )
    )

## See Also

* [Basic Usage by the MultiSelect HtmlHelper for ASP.NET Core (Demo)](https://demos.telerik.com/aspnet-core/multiselect/index)
* [Using the API of the MultiSelect HtmlHelper for ASP.NET Core (Demo)](https://demos.telerik.com/aspnet-core/multiselect/api)
* [JavaScript API Reference of the MultiSelect](http://docs.telerik.com/kendo-ui/api/javascript/ui/multiselect)
