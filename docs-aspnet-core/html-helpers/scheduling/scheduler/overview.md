---
title: Overview
page_title: Scheduler Overview | Telerik UI for ASP.NET Core HtmlHelpers
description: "Learn the basics when working with the Kendo UI Scheduler HtmlHelper for ASP.NET Core (MVC 6 or ASP.NET Core MVC)."
previous_url: /aspnet-core/helpers/html-helpers/scheduler
slug: htmlhelpers_scheduler_aspnetcore
position: 1
---

# Scheduler HtmlHelper Overview

The [Scheduler](http://docs.telerik.com/kendo-ui/controls/scheduling/scheduler/overview) displays a set of events, appointments, or tasks.

It support the display of scheduled events in different views&mdash;single days, whole weeks, or months, or as a list of tasks which need to be accomplished.

The Scheduler HtmlHelper extension is a server-side wrapper for the [Kendo UI Scheduler](http://demos.telerik.com/kendo-ui/scheduler/index) widget. For more information on the Scheduler HtmlHelper, refer to the [UI for ASP.NET MVC documentation](https://docs.telerik.com/aspnet-mvc/helpers/scheduler/overview).

> As of the Kendo UI R1 2017 release, exceptions are no longer automatically removed when the user edits a series. Changes that are made to specific occurrences are persisted during series editing. If a series contains an exception, the Scheduler renders a **Reset Series** button within the **Edit** dialog of the series which allows the user to reset the series by removing existing exceptions.

## Initializing the Scheduler

The following example demonstrates how to define the Scheduler by using the Scheduler HtmlHelper.

```Razor
    @(Html.Kendo().Scheduler<Kendo.Mvc.Examples.Models.Scheduler.TaskViewModel>()
        .Name("scheduler")
        .Date(new DateTime(2013, 6, 13))
        .StartTime(new DateTime(2013, 6, 13, 7, 00, 00))
        .Height(600)
        .Views(views =>
        {
            views.DayView();
            views.WeekView(weekView => weekView.Selected(true));
            views.TimelineView();
        })
        .Timezone("Etc/UTC")
        .DataSource(d => d
            .Model(m =>
            {
                m.Id(f => f.TaskID);
                m.RecurrenceId(f => f.RecurrenceID);
                m.Field(f => f.Title).DefaultValue("No title");
                m.Field(f => f.OwnerID).DefaultValue(1);
                m.Field(f => f.Title).DefaultValue("No title");
            })
            .Read("Read", "Scheduler")
            .Create("Create", "Scheduler")
            .Destroy("Destroy", "Scheduler")
            .Update("Update", "Scheduler")
        )
    )
```
```Controller
    public class SchedulerController : Controller
    {
        private ISchedulerEventService<TaskViewModel> taskService;

        public SchedulerController(
            ISchedulerEventService<TaskViewModel> schedulerTaskService)
        {
            taskService = schedulerTaskService;
        }

        public IActionResult Index()
        {
            return View();
        }

        public virtual JsonResult Read([DataSourceRequest] DataSourceRequest request)
        {
            return Json(taskService.GetAll().ToDataSourceResult(request));
        }

        public virtual JsonResult Destroy([DataSourceRequest] DataSourceRequest request, TaskViewModel task)
        {
            if (ModelState.IsValid)
            {
                taskService.Delete(task, ModelState);
            }

            return Json(new[] { task }.ToDataSourceResult(request, ModelState));
        }

        public virtual JsonResult Create([DataSourceRequest] DataSourceRequest request, TaskViewModel task)
        {
            if (ModelState.IsValid)
            {
                taskService.Insert(task, ModelState);
            }

            return Json(new[] { task }.ToDataSourceResult(request, ModelState));
        }

        public virtual JsonResult Update([DataSourceRequest] DataSourceRequest request, TaskViewModel task)
        {
            //example custom validation:
            if (task.Start.Hour < 8 || task.Start.Hour > 22)
            {
                ModelState.AddModelError("start", "Start date must be in working hours (8h - 22h)");
            }

            if (ModelState.IsValid)
            {
                taskService.Update(task, ModelState);
            }

            return Json(new[] { task }.ToDataSourceResult(request, ModelState));
        }
    }
```

## Basic Configuration

The following example demonstrates the basic configuration of the Scheduler HtmlHelper.


The following example demonstrates the basic configuration of the Scheduler HtmlHelper.

```
    @(Html.Kendo().Scheduler<Kendo.Mvc.Examples.Models.Scheduler.MeetingViewModel>()
        .Name("scheduler")
        .CurrentTimeMarker(true)
        .Editable(true)
        .Date(new DateTime(2013, 6, 13))
        .Pdf(pdf => pdf
            .FileName("SchedulerExport.pdf")
            .ProxyURL(Url.Action("Pdf_Export_Save", "Scheduler"))
        )
        .Timezone("Etc/UTC")
        .Toolbar(t => t.Pdf())
        .StartTime(new DateTime(2013, 6, 13, 7, 00, 00))
        .Height(600)
        .Views(views =>
        {
            views.DayView();
            views.WeekView();
            views.MonthView(monthView => monthView.Selected(true));
            views.AgendaView();
            views.TimelineView();
        })
        .Group(group => { group.Resources("Rooms"); group.Date(true); })
        .Resources(resource =>
        {
            resource.Add(m => m.RoomID)
                .Title("Room")
                .Name("Rooms")
                .DataTextField("Text")
                .DataValueField("Value")
                .DataColorField("Color")
                .BindTo(new[] {
                        new { Text = "Meeting Room 101", Value = 1, Color = "#6eb3fa" },
                        new { Text = "Meeting Room 201", Value = 2, Color = "#f58a8a" }
                });

        })
        .DataSource(d => d
                .Model(m =>
                {
                    m.Id(f => f.MeetingID);
                    m.Field(f => f.Title).DefaultValue("No title");
                    m.RecurrenceId(f => f.RecurrenceID);
                    m.Field(f => f.Title).DefaultValue("No title");
                })
                .Read("Date_Grouping_Read", "Scheduler")
                .Create("Date_Grouping_Create", "Scheduler")
                .Destroy("Date_Grouping_Destroy", "Scheduler")
                .Update("Date_Grouping_Update", "Scheduler")
        )
    )
```

## Functionality and Features

The Scheduler provides options for [adaptive rendering]({% slug htmlhelpers_scheduler_adaptiverendering_aspnetcore %}).

## Events

You can subscribe to all Scheduler [events](http://docs.telerik.com/kendo-ui/api/javascript/ui/scheduler#events). For a complete example on basic Scheduler events, refer to the [demo on using the events of the Scheduler](https://demos.telerik.com/aspnet-core/scheduler/events). For a runnable example on the `move` and `resize` events, refer to the [demo on the specific events](https://demos.telerik.com/aspnet-core/scheduler/move-resize).

The following example demonstrates how to subscribe to the `dataBound` and `dataBinding` events.

```Razor
    @(Html.Kendo().Scheduler<KendoUISchedulerDemo.Models.Projection>()
        .Name("scheduler")
        .Date(new DateTime(2013, 6, 13))
        .StartTime(new DateTime(2013, 6, 13, 10, 00, 00))
        .EndTime(new DateTime(2013, 6, 13, 23, 00, 00))
        .Editable(false)
        .Height(600)
        .BindTo(Model)
        .Events(e => {
            e.DataBound("scheduler_dataBound");
            e.DataBinding("scheduler_dataBinding");
        })
    )

    <script>
        function scheduler_dataBound(e) {
            //Handle the dataBound event.
        }

        function scheduler_dataBinding(e) {
            //Handle the dataBinding event.
        }
    </script>
```

## Referencing Existing Instances

To reference an existing Kendo UI Scheduler instance, use the [`jQuery.data()`](http://api.jquery.com/jQuery.data/) configuration option. Once a reference is established, use the [Scheduler API](http://docs.telerik.com/kendo-ui/api/javascript/ui/scheduler#methods) to control its behavior.

    // Place this after your Kendo UI Scheduler for ASP.NET Core declaration.
    <script>
        $(document).ready(function() {
            // The Name() of the Scheduler is used to get its client-side instance.
            var scheduler = $("#scheduler").data("kendoScheduler");
        });
    </script>

## See Also

* [Basic Usage of the Scheduler HtmlHelper for ASP.NET Core (Demo)](https://demos.telerik.com/aspnet-core/scheduler)
* [Using the API of the Scheduler HtmlHelper for ASP.NET Core (Demo)](https://demos.telerik.com/aspnet-core/scheduler/api)
* [JavaScript API Reference of the Scheduler](http://docs.telerik.com/kendo-ui/api/javascript/ui/scheduler)
