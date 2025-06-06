---
title: "CSSStyleValue: parse() static method"
short-title: parse()
slug: Web/API/CSSStyleValue/parse_static
page-type: web-api-static-method
browser-compat: api.CSSStyleValue.parse_static
---

{{APIRef("CSS Typed Object Model API")}}

The **`parse()`** static method of the {{domxref("CSSStyleValue")}}
interface sets a specific CSS property to the specified values and returns the first
value as a {{domxref('CSSStyleValue')}} object.

## Syntax

```js-nolint
CSSStyleValue.parse(property, cssText)
```

### Parameters

- `property`
  - : A CSS property to set.
- `cssText`
  - : A comma-separated string containing one or more values to apply to the provided
    property.

### Return value

A `CSSStyleValue` object containing the first supplied value.

## Examples

The code below parses a set of declarations for the `transform` property.
The second code block shows the structure of the returned object as it would be rendered
in a developer tools console.

```js
const css = CSSStyleValue.parse(
  "transform",
  "translate3d(10px,10px,0) scale(0.5)",
);
```

```plain
CSSTransformValue {0: CSSTranslate, 1: CSSScale, length: 2, is2D: false}
```

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- [`CSSStyleValue.parseAll()`](/en-US/docs/Web/API/CSSStyleValue/parseAll_static)

- [Using the CSS Typed OM](/en-US/docs/Web/API/CSS_Typed_OM_API/Guide)
- [CSS Typed Object Model API](/en-US/docs/Web/API/CSS_Typed_OM_API)
