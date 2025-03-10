---
title:  Keyboard Navigation
page_title: Keyboard Navigation | Kendo UI ContextMenu HtmlHelper for ASP.NET Core
description: "Learn how to use the keyboard navigation functionality of the Kendo UI ContextMenu HtmlHelper for ASP.NET Core (MVC 6 or ASP.NET Core MVC)."
slug: htmlhelpers_contextmenu_keyboardnavigation_aspnetcore
position: 3
---

# Keyboard Navigation

The keyboard navigation of the ContextMenu is always available.

When the ContextMenu is focused, the first root item is activated.

The ContextMenu supports the following keyboard shortcuts:

| SHORTCUT						| DESCRIPTION				                                                        |
|:---                 |:---                                                                               |
| `Home`              | Focuses the first item.                                                            |
| `End`               | Focuses the last item.                                                             |
| `Left Arrow`        | <ul><li>Moves the active item on the root level of a horizontal ContextMenu to the left.</li> <li>Closes an item group.</li></ul> |
| `Right Arrow`       | <ul><li>Moves the active item on the root level of a horizontal ContextMenu to the right.</li> <li>Opens an item group of a vertical ContextMenu.</li> <li>If the previous active item has been inside an item group, moves the active state to the next root item of a horizontal ContextMenu.</li></ul>        |
| `Up Arrow`          | Moves upwards the active item of a vertical ContextMenu item group.                        |
| `Down Arrow`        | <ul><li>Moves downwards the active item of a vertical ContextMenu item group.</li> <li>Opens an item group of a horizontal ContextMenu.</li></ul> |
| `Enter`             | Selects or navigates the focused item.                                             |
| `Space`             | Selects or navigates the focused item.                                             |
| `Esc`               | Closes an item group.                                                              |
| (`Shift`+) `Tab`    | Blurs the ContextMenu and moves the focus to the next or previous focusable element on the page.  |

## See Also

* [JavaScript API Reference of the ContextMenu](https://docs.telerik.com/kendo-ui/api/javascript/ui/contextmenu)
* [ContextMenu Official Demo](https://demos.telerik.com/aspnet-core/menu/context-menu)