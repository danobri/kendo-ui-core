---
title: Overview
page_title: Upload Overview | Telerik UI for ASP.NET Core Tag Helpers
description: "Learn the basics when working with the Kendo UI Upload tag helper for ASP.NET Core (MVC 6 or ASP.NET Core MVC)."
previous_url: /aspnet-core/helpers/upload, /aspnet-core/helpers/tag-helpers/upload
slug: taghelpers_upload_aspnetcore
position: 1
---

# Upload Tag Helper Overview

The [Upload](http://docs.telerik.com/kendo-ui/controls/editors/upload/overview) uses progressive enhancement to deliver the best possible uploading experience to users, without requiring extra developer effort.

The Upload tag helper extension is a server-side wrapper for the [Kendo UI Upload](https://demos.telerik.com/kendo-ui/upload/index) widget and enables you to configure the Kendo UI Upload widget in ASP.NET Core applications.

## Initializing the Upload

The following example demonstrates how to define the Upload by using the Upload tag helper.

> To ensure the tag-naming consistency across the Telerik UI for ASP.NET Core suite, the Kendo UI R1 2018 release introduces a change in the tag names of the Upload. As of the Kendo UI R1 2018 release:
> * The `<kendo-upload-async-settings>` tag name is changed to `<async>`
> * The `<kendo-upload-files>` tag name is changed to `<files>`.
> * The `<kendo-upload-file>` tag name is changed to `<file>`.
> * The `<kendo-upload-localization-settings>` tag name is changed to `<localization>`.
> * The `<kendo-upload-validation-settings>` tag name is changed to `<validation>`.

        <kendo-upload drop-zone="drop-zone1" name="test">
            <async auto-upload="true" />
            <validation allowed-extensions="@Model.Extensions" />
            <files>
                <file name="dummy" size="1024" />
            </files>
        </kendo-upload>

## Basic Configuration

The Upload tag helper configuration options are passed as attributes of the tag or attributes of the nested composite and collection properties.

```cshtml

        @(Html.Kendo().Upload()
            .Name("upload1")
            .DropZone("drop-zone1")
            .Validation(v => v.AllowedExtensions(Model.Extensions))
            .Files(f => f.Add().Name("dummy").Size(1024))
    )
```
```tagHelper
        <kendo-upload drop-zone="drop-zone1" name="test">
            <async auto-upload="true" />
            <validation allowed-extensions="@Model.Extensions" />
            <files>
                <file name="dummy" size="1024" />
            </files>
        </kendo-upload>
```

## See Also

* [Basic Usage of the Upload Tag Helper for ASP.NET Core (Demo)](https://demos.telerik.com/aspnet-core/upload/tag-helper)
* [JavaScript API Reference of the Upload](https://docs.telerik.com/kendo-ui/api/javascript/ui/upload)
