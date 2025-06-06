---
title: <linearGradient>
slug: Web/SVG/Reference/Element/linearGradient
page-type: svg-element
browser-compat: svg.elements.linearGradient
sidebar: svgref
---

The **`<linearGradient>`** [SVG](/en-US/docs/Web/SVG) element lets authors define linear gradients to apply to other SVG elements.

## Usage context

{{svginfo}}

## Attributes

- {{SVGAttr("gradientUnits")}}
  - : This attribute defines the coordinate system for attributes `x1`, `x2`, `y1`, `y2`
    _Value type_: `userSpaceOnUse` | `objectBoundingBox`; _Default value_: `objectBoundingBox`; _Animatable_: **yes**
- {{SVGAttr("gradientTransform")}}
  - : This attribute provides additional [transformation](/en-US/docs/Web/SVG/Reference/Attribute/transform) to the gradient coordinate system.
    _Value type_: [**\<transform-list>**](/en-US/docs/Web/SVG/Guides/Content_type#transform-list); _Default value_: _identity transform_; _Animatable_: **yes**
- {{SVGAttr("href")}}
  - : This attribute defines a reference to another `<linearGradient>` element that will be used as a template.
    _Value type_: [**\<URL>**](/en-US/docs/Web/SVG/Guides/Content_type#url); _Default value_: none; _Animatable_: **yes**
- {{SVGAttr("spreadMethod")}}
  - : This attribute indicates how the gradient behaves if it starts or ends inside the bounds of the shape containing the gradient.
    _Value type_: `pad` | `reflect` | `repeat`; _Default value_: `pad`; _Animatable_: **yes**
- {{SVGAttr("x1")}}
  - : This attribute defines the x coordinate of the starting point of the vector gradient along which the linear gradient is drawn.
    _Value type_: [**\<length>**](/en-US/docs/Web/SVG/Guides/Content_type#length); _Default value_: `0%`; _Animatable_: **yes**
- {{SVGAttr("x2")}}
  - : This attribute defines the x coordinate of the ending point of the vector gradient along which the linear gradient is drawn.
    _Value type_: [**\<length>**](/en-US/docs/Web/SVG/Guides/Content_type#length); _Default value_: `100%`; _Animatable_: **yes**
- {{SVGAttr("xlink:href")}} {{deprecated_inline}}
  - : An [\<IRI>](/en-US/docs/Web/SVG/Guides/Content_type#iri) reference to another `<linearGradient>` element that will be used as a template.
    _Value type_: [**\<IRI>**](/en-US/docs/Web/SVG/Guides/Content_type#iri); _Default value_: none; _Animatable_: **yes**
- {{SVGAttr("y1")}}
  - : This attribute defines the y coordinate of the starting point of the vector gradient along which the linear gradient is drawn.
    _Value type_: [**\<length>**](/en-US/docs/Web/SVG/Guides/Content_type#length); _Default value_: `0%`; _Animatable_: **yes**
- {{SVGAttr("y2")}}
  - : This attribute defines the y coordinate of the ending point of the vector gradient along which the linear gradient is drawn.
    _Value type_: [**\<length>**](/en-US/docs/Web/SVG/Guides/Content_type#length); _Default value_: `0%`; _Animatable_: **yes**

## DOM Interface

This element implements the {{domxref("SVGLinearGradientElement")}} interface.

## Example

```css hidden
html,
body,
svg {
  height: 100%;
}
```

```html
<svg
  viewBox="0 0 10 10"
  xmlns="http://www.w3.org/2000/svg"
  xmlns:xlink="http://www.w3.org/1999/xlink">
  <defs>
    <linearGradient id="myGradient" gradientTransform="rotate(90)">
      <stop offset="5%" stop-color="gold" />
      <stop offset="95%" stop-color="red" />
    </linearGradient>
  </defs>

  <!-- using my linear gradient -->
  <circle cx="5" cy="5" r="4" fill="url('#myGradient')" />
</svg>
```

{{EmbedLiveSample('Example', 150, '100%')}}

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}
