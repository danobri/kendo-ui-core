---
title: Validation
page_title: Validation | Kendo UI MaskedTextBox for ASP.NET Core HtmlHelpers
description: "Use the predefined and custom masks in the Kendo UI MaskedTextBox for ASP.NET Core (MVC 6 or ASP.NET Core MVC)."
slug: validation_maskedtextbox_aspnetcore
position: 2
---

# Validation

The MaskedTextBox provides a set of predefined mask rules and enables you to modify them.

## Predefined Masks

> If no mask is defined, the widget allows any input.

The MaskedTextBox has [a list of predefined mask rules](http://docs.telerik.com/kendo-ui/controls/editors/maskedtextbox/overview#configuration-Rules) which can be used to compose the mask of a widget.

The following example demonstrates how to set a `zip code` mask.

```
    @(Html.Kendo().MaskedTextBox()
          .Name("maskedtextbox")
          .Mask("00000-9999") // Set the zip code.
    )
```

## Custom Masks

The MaskedTextBox enables you to define custom mask rules if none of the predefined ones is suitable. To add a custom rule, use the `Rules` method.

> The widget supports [JavaScript Regular Expressions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) defined as a string or a JavaScript function.

The following example demonstrates how to define a custom rule for the `-` (minus) and `+` (plus) symbols.

```
  @(Html.Kendo().MaskedTextBox()
        .Name("maskedtextbox")
        .Rules(rules => {
            rules.Add('~', "/[+-]/");
        })
        .Mask("~0000") // Set a mask with a custom rule.
   )
```

## See Also

* [JavaScript API Reference of the MaskedTextBox](http://docs.telerik.com/kendo-ui/api/javascript/ui/maskedtextbox)
