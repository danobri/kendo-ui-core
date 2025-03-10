---
title: Server Binding
page_title: Server Binding | Telerik UI for ASP.NET Core Scheduler HtmlHelper
description: "Get started with the Scheduler HtmlHelper for ASP.NET Core and learn how to bind it to a model."
slug: htmlhelpers_scheduler_serverbinding_aspnetcore
position: 2
---

# Server Binding

The steps below demonstrate how to bind the Scheduler to a model.

1. Make sure you followed all the steps from the [Getting Started]({% slug gettingstarted_aspnetmvc6_aspnetmvc %}) article on Telerik UI for ASP.NET Core.

1. Create a new model, which inherits the `ISchedulerEvent` interface.

    ###### Example

        public class Projection : ISchedulerEvent
        {
            public string Title { get; set; }
            public DateTime Start { get; set; }
            public DateTime End { get; set; }
            public string Description { get; set; }
            public bool IsAllDay { get; set; }
            string StartTimezone { get; set; }
            string EndTimezone { get; set; }
            public string RecurrenceRule { get; set; }
            public string RecurrenceException { get; set; }
        }

1. Create a new action method which passes the `List` of projections to the view.

    ###### Example

        public IActionResult Index()
        {
            List<Projection> cinemaSchedule = new List<Projection> {
                new Projection {
                    Title = "Fast and furious 6",
                    Start = new DateTime(2013,6,13,17,00,00),
                    End= new DateTime(2013,6,13,18,30,00)
                },
                new Projection {
                    Title= "The Internship",
                    Start= new DateTime(2013,6,13,14,00,00),
                    End= new DateTime(2013,6,13,15,30,00)
                },
                new Projection {
                    Title = "The Perks of Being a Wallflower",
                    Start =  new DateTime(2013,6,13,16,00,00),
                    End =  new DateTime(2013,6,13,17,30,00)
                }};

            return View(cinemaSchedule);
        }

1. Add a Scheduler.

    ```Razor
        @(Html.Kendo().Scheduler<KendoUISchedulerDemo.Models.Projection>()
            .Name("scheduler")
            .Date(new DateTime(2013, 6, 13))
            .StartTime(new DateTime(2013, 6, 13, 10, 00, 00))
            .EndTime(new DateTime(2013, 6, 13, 23, 00, 00))
            .Editable(false)
            .Height(600)
            .BindTo(Model)
        )
    ```


## See Also

* [Overview of the Scheduler HtmlHelper]({% slug htmlhelpers_scheduler_aspnetcore %})
* [Ajax Binding of the Scheduler HtmlHelper]({% slug htmlhelpers_scheduler_ajaxbinding_aspnetcore %})
* [Telerik UI for ASP.NET MVC Troubleshooting]({% slug knownissues_aspnetmvc6_aspnetmvc %})
