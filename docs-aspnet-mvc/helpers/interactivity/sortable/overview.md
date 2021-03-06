---
title: Overview
page_title: Sortable Overview | Telerik UI for ASP.NET MVC HTML Helpers
description: "Learn the basics when working with the Telerik UI Sortable widget for ASP.NET MVC."
slug: overview_sortablehelper_aspnetmvc
position: 1
---

# Sortable HtmlHelper Overview

The Telerik UI Sortable HtmlHelper for ASP.NET Core is a server-side wrapper for the Kendo UI Sortable widget.

The Sortable provides a sortable drag-and-drop functionality to elements within a list. Unlike most of the Telerik UI HtmlHelpers for ASP.NET MVC, the Sortable does not render HTML markup. You have to initialize it for a DOM element which already exists.

* [Demo page for the Sortable](https://demos.telerik.com/aspnet-mvc/sortable)

## Basic Configuration

1. Make sure you followed all the steps from the [introductory article on Telerik UI for ASP.NET MVC]({% slug overview_aspnetmvc %}).
1. Create a new action method.

        public ActionResult Index()
        {
            return View();
        }

1. Initialize the Sortable.

    ```ASPX
        <ul id="sortable-basic">
            <li class="sortable">Papercut <span>3:04</span></li>
            <li class="sortable">One Step Closer <span>2:35</span></li>
            <li class="sortable">With You <span>3:23</span></li>
        </ul>
        <%:Html.Kendo().Sortable()
            .For("#sortable-basic") // The for option of the Sortable is mandatory.
                                    // It is a jQuery selector which specifies.
                                    // The already existing element for which the Sortable will be initialized.
            .HintHandler("hint") // The JavaScript function which
                                // constructs the hint element of the Sortable.
            .PlaceholderHandler("placeholder") // The JavaScript function which
                                                //constructs the placeholder element of the Sortable.
        %>
        <script>
            // Define the hint handler.
            function hint(element) {
                return element.clone().addClass("hint");
            }
            // Define the placeholder handler.
            function placeholder(element) {
                return element.clone().addClass("placeholder").text("drop here");
            }
        </script>
    ```
    ```Razor
        <ul id="sortable-basic">
            <li class="sortable">Papercut <span>3:04</span></li>
            <li class="sortable">One Step Closer <span>2:35</span></li>
            <li class="sortable">With You <span>3:23</span></li>
        </ul>
        @(Html.Kendo().Sortable()
            .For("#sortable-basic") // The for option of the Sortable is mandatory.
                                    // It is a jQuery selector which specifies
                                    // The already existing element for which the Sortable will be initialized.
            .HintHandler("hint") // The JavaScript function which
                                // constructs the hint element of the Sortable.
            .PlaceholderHandler("placeholder") // The JavaScript function which
                                                // constructs the placeholder element of the Sortable.
        )
        <script>
            // Define the hint handler.
            function hint(element) {
                return element.clone().addClass("hint");
            }
            // Define the placeholder handler.
            function placeholder(element) {
                return element.clone().addClass("placeholder").text("drop here");
            }
        </script>
    ```

The Sortable enables you to disable its hint by setting it to an empty [`jQuery.noop`](http://api.jquery.com/jQuery.noop/) function.

    @(Html.Kendo().Sortable()
        .For("#sortable")
        .HintHandler("noHint")
    )

    <script>
        var noHint = $.noop;
    </script>

## Events

You can subscribe to all Sortable [events](/api/sortable). For a complete example on basic Sortable events, refer to the [demo on using the events of the Sortable](https://demos.telerik.com/aspnet-mvc/sortable/events).

### Handling by Handler Name

The following example demonstrates how to subscribe to events by a handler name.

```ASPX
    <ul id="sortable">
        <li>Item 1</li>
        <li>Item 2</li>
        <li>Item 3</li>
    </ul>
    <%:Html.Kendo().Sortable()
        .For("#sortable")
        .Events(events => events
            .Start("onStart")
            .Change("onChange")
        )
    %>
    <script>
        function onStart(e) {
            var id = e.sender.element.attr("id");
            kendoConsole.log(id + " start: " + e.item.text());
        }

        function onChange(e) {
            var id = e.sender.element.attr("id"),
                text = e.item.text(),
                newIndex = e.newIndex,
                oldIndex = e.oldIndex;

            kendoConsole.log(id + " change: " + text + " newIndex: " + newIndex + " oldIndex: " + oldIndex + " action: " + e.action);
        }
    </script>
```
```Razor
    <ul id="sortable">
        <li>Item 1</li>
        <li>Item 2</li>
        <li>Item 3</li>
    </ul>
    @(Html.Kendo().Sortable()
        .For("#sortable")
        .Events(events => events
            .Start("onStart")
            .Change("onChange")
        )
    )
    <script>
        function onStart(e) {
            var id = e.sender.element.attr("id");
            kendoConsole.log(id + " start: " + e.item.text());
        }

        function onChange(e) {
            var id = e.sender.element.attr("id"),
                text = e.item.text(),
                newIndex = e.newIndex,
                oldIndex = e.oldIndex;

            kendoConsole.log(id + " change: " + text + " newIndex: " + newIndex + " oldIndex: " + oldIndex + " action: " + e.action);
        }
    </script>
```

### Handling by Template Delegate

The following example demonstrates how to subscribe to events by a template delegate.

    <ul id="sortable">
        <li>Item 1</li>
        <li>Item 2</li>
        <li>Item 3</li>
    </ul>
    @(Html.Kendo().Sortable()
        .For("#sortable")
        .Events(events => events
            .Start(@<text>
                function() {
                    // Handle the show event inline.
                }
            </text>)
            .Change(@<text>
                function() {
                    // Handle the show event inline.
                }
            </text>)
        )
    )

## Referencing Existing Instances

To reference an existing Sortable instance, use the [`jQuery.data()`](http://api.jquery.com/jQuery.data/) configuration option. Once a reference is established, use the [Sortable client-side API](http://docs.telerik.com/kendo-ui/api/javascript/ui/sortable#methods) to control its behavior.

    // Place the following after the Sortable for ASP.NET MVC declaration.
    <script>
        $(function() {
            // The For() of the Sortable is used to get its client-side instance.
            var sortable = $("#container").data("kendoSortable");
        });
    </script>

## See Also

* [Basic Usage of the Sortable HtmlHelper for ASP.NET MVC (Demo)](https://demos.telerik.com/aspnet-mvc/sortable/index)
* [SortableBuilder Server-Side API](http://docs.telerik.com/aspnet-mvc/api/Kendo.Mvc.UI.Fluent/SortableBuilder)
* [Sortable Server-Side API](/api/sortable)
