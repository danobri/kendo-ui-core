---
title: Overview
page_title: StockChart Overview | Telerik UI for ASP.NET Core HtmlHelpers
description: "Learn the basics when working with the Kendo UI StockChart HtmlHelper for ASP.NET Core (MVC 6 or ASP.NET Core MVC)."
slug: overview_stockcharthelper_aspnetcore
position: 1
---

# StockChart HtmlHelper Overview

The Kendo UI Stock Chart is a specialized control visualizing the price movement of any financial instrument over a certain period of time.

The StockChart HtmlHelper extension is a server-side wrapper for the [Kendo UI StockChart](https://demos.telerik.com/kendo-ui/financial/index) widget. For more information on the StockChart HtmlHelper for ASP.NET MVC, refer to the [UI for ASP.NET MVC documentation](https://docs.telerik.com/aspnet-mvc/helpers/stockchart/overview).

## Data Binding

The UI for ASP.NET StockChart makes Ajax requests when bound to a data source.

To configure the StockChart for Ajax binding:

1. Add the new action method.  

    The following example demonstrates how to add a new action method which returns data to populate the StockChart.

        ```Razor
            @(Html.Kendo().StockChart<Kendo.Mvc.Examples.Models.StockDataPoint>()
                .Name("stockChart")
                .Title("The Boeing Company (NYSE:BA)")
                .DataSource(ds => ds.Read(read => read
                    .Action("_BoeingStockData", "Home")
                ))
                .DateField("Date")
            )
        ```
        ```Model
            public class StockDataPoint
            {
                public DateTime Date { get; set; }

                public decimal Close { get; set; }

                public long Volume { get; set; }

                public decimal Open { get; set; }

                public decimal High { get; set; }

                public decimal Low { get; set; }

                public string Symbol { get; set; }
            }
        ```
        ```HomeController
            public IActionResult Index()
            {
                return View();
            }

            public IActionResult _BoeingStockData()
            {
                using (var db = GetContext())
                {
                    // Return the data as JSON.
                    return Json(
                        (from s in db.Stocks
                        where s.Symbol == "BA"
                        select new StockDataPoint
                        {
                            Date = s.Date,
                            Open = s.Open,
                            High = s.High,
                            Low = s.Low,
                            Close = s.Close,
                            Volume = s.Volume
                        }).ToList()
                    );
                }
            }
        ```

1. Create the data series.

    The following example demonstrates how to create the main and the navigator data series.

        ```
            @(Html.Kendo().StockChart<Kendo.Mvc.Examples.Models.StockDataPoint>()
                .Name("stockChart")
                .Title("The Boeing Company (NYSE:BA)")
                .DataSource(ds => ds.Read(read => read
                    .Action("_BoeingStockData", "Home")
                ))
                .DateField("Date")
                        .Series(series => {
                    series.Candlestick(s => s.Open, s => s.High, s => s.Low, s => s.Close);
                })
                .Navigator(nav => nav
                    .Series(series => {
                        series.Line(s => s.Volume);
                    })
                )
            )
        ```

## Events

You can subscribe to all StockChart [events](https://docs.telerik.com/kendo-ui/api/javascript/dataviz/ui/stock-chart#events).

### Handling Events by Handler Name

The following example demonstrates how to subscribe to events by a handler name.

```
    @(Html.Kendo().StockChart(Model)
    	.Name("stockChart")
    	.Title("The Boeing Company (NYSE:BA)")
    	.DateField("Date")
    	.Series(series => {
    	    series.Candlestick(s => s.Open, s => s.High, s => s.Low, s => s.Close);
    	})
    	.Events(e => e
    	  .DataBound("stockChart_dataBound")
    	  .SeriesClick("stockChart_seriesClick")
    	)
    )

    <script>
        function stockChart_dataBound(e) {
            //Handle the dataBound event.
        }

        function stockChart_seriesClick(e) {
            //Handle the seriesClick event.
        }
    </script>
```

### Handling Events by Template Delegate

The following example demonstrates how to subscribe to events by a template delegate.

```
    @(Html.Kendo().StockChart(Model)
    	.Name("stockChart")
    	.Title("The Boeing Company (NYSE:BA)")
    	.DateField("Date")
    	.Series(series => {
    	    series.Candlestick(s => s.Open, s => s.High, s => s.Low, s => s.Close);
    	})
    	.Events(e => e
    	  .DataBound(@<text>
    	       function(e) {
    	           //Handle the dataBound event inline.
    	       }
    	  </text>)
    	  .SeriesClick(@<text>
    	       function(e) {
    	           //Handle the seriesClick event inline.
    	       }
    	  </text>)
    	)
    )
```

## Referencing Existing Instances

To reference an existing Kendo UI StockChart instance, use the [`jQuery.data()`](https://api.jquery.com/jQuery.data/) configuration option. Once a reference is established, use the [StockChart API](https://docs.telerik.com/kendo-ui/api/javascript/dataviz/ui/stock-chart#methods) to control its behavior.

    // Place the following after the declaration of the Barcode for ASP.NET Core.
    <script>
        $(function() {
            // The Name() of the StockChart is used to get its client-side instance.
            var chart = $("#stockChart").data("kendoStockChart");
        });
    </script>

## See Also

* [Basic Usage of the StockChart HtmlHelper for ASP.NET Core (Demo)](https://demos.telerik.com/aspnet-core/financial/index)
* [Basic Usage of the Kendo UI StockChart Widget (Demo)](https://demos.telerik.com/kendo-ui/financial/index)
* [JavaScript API Reference of the Kendo UI StockChart](https://docs.telerik.com/kendo-ui/api/javascript/dataviz/ui/stock-chart)
