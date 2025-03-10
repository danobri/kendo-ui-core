---
title: Add Background Color to Sorted Columns by Using LESS Themes
page_title: Add Background Color with LESS Themes | Kendo UI Grid for jQuery
description: "An example on how to add a background color to the sorted columns of the Kendo UI Grid for jQuery by using the LESS themes."
previous_url: /controls/data-management/grid/how-to/Layout/add-background-sorted-columns-LESS-themes
slug: howto_add_background_sorted_columns_LESS_themes_grid
tags: backaground, color, less, themes, columns, grid
component: grid
type: how-to
res_type: kb
---

## Environment

<table>
 <tr>
  <td>Product</td>
  <td>Progress Kendo UI for jQuery</td>
 </tr>
</table>

## Description

How can I add a background color to the sorted columns of the Grid by using the [LESS themes]({% slug themesandappearnce_kendoui_desktopwidgets %})?

## Solution

To achieve this behavior:

1. Change the default background of the alternate row to an RGBA color format with a low opaque level.
1. Add the background color to the `.k-sorted` class by using the RGBA color format.

> * The `.k-sorted` class is available as of the Kendo UI 2017 R2 SP1 release.
> * If you do not override the `k-alt` class, the background color of the `.k-sorted` class will not apply.

The following examples demonstrate how to change the background color of selected rows in a Grid when working with:

* [Dark themes](#dark-themes)
* [Light themes](#light-themes)

### Dark Themes

When your project uses a dark theme, use light colors for the background of the selected rows.

The following example demonstrates how to apply the suggested background colors to the selected Grid rows if your project uses the Black or Material Black theme.  

```tab-Black
    .k-grid .k-alt {
        background-color: rgba(255, 255, 255, 0.04);
    }
    col.k-sorted, th.k-sorted {
        background-color: rgba(255, 255, 255, 0.2);
    }
```
```tab-MaterialBlack
    .k-grid .k-alt {
        background-color: rgba(255, 255, 255, 0);
    }
    col.k-sorted, th.k-sorted {
        background-color: rgba(255, 255, 255, 0.1);
    }
```

### Light Themes

When your project uses a light theme, use dark colors for the background of the selected rows.

The following example demonstrates how to apply the suggested background colors to the selected Grid rows if your project uses the Default or Material theme.

```tab-Default
    .k-grid .k-alt {
        background-color: rgba(0, 0, 0, 0.06);
    }
    col.k-sorted, th.k-sorted {
        background-color: rgba(0, 0, 0, 0.1);
    }
```
```tab-Material
    .k-grid .k-alt {
        background-color: rgba(0, 0, 0, 0);
    }
    col.k-sorted, th.k-sorted {
        background-color: rgba(0, 0, 0, 0.1);
    }
```

## See Also

* [JavaScript API Reference of the Grid](/api/javascript/ui/grid)
