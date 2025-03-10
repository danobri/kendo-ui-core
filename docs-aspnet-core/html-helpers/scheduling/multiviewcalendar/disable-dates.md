---
title: Disabled Dates
page_title: Disabled Dates | Kendo UI MultiViewCalendar HtmlHelper for ASP.NET Core
description: "Learn how to disable dates in the Kendo UI MultiViewCalendar widget."
slug: disabled_dates_multiviewcalendar_htmlhelper_aspnetcore
position: 6
---

# Disabled Dates

The MultiViewCalendar allows you to disable certain days which are not intended to be selected by the end user such as weekends, national holidays, and others.

To disable a date, either [set an array](#setting-and-array) or [add a function](#adding-a-function).

## Setting an Array

When you set an array, list the days that need to be disabled by using the first letters from their names in English.

```Razor

        @(Html.Kendo().MultiViewCalendar()
            .Name("MultiViewCalendar")
            .DisableDates(new[] {"we", "th" })
        )
```

## Adding a Function

When you add a function, determine its return value as `true` for the date that is disabled.

```Razor

        @(Html.Kendo().MultiViewCalendar()
            .Name("MultiViewCalendar")
            .DisableDates("handler")
        )

        <script>
            function handler(date) {
                var disabled = [13,14,20,21];
                if (date && disabled.indexOf(date.getDate()) > -1 ) {
                    return true;
                } else {
                    return false;
                }
            }
        </script>
```

## See Also

* [Disabled Dates in the MultiViewCalendar HtmlHelper for ASP.NET Core (Demo)](https://demos.telerik.com/aspnet-core/multiviewcalendar/disabled-dates)
* [JavaScript API Reference of the MultiViewCalendar](http://docs.telerik.com/kendo-ui/api/javascript/ui/multiviewcalendar)
