---
title: <title> — the SVG accessible name element
slug: Web/SVG/Reference/Element/title
page-type: svg-element
browser-compat: svg.elements.title
sidebar: svgref
---

The **`<title>`** [SVG](/en-US/docs/Web/SVG) element provides an accessible, short-text description of any SVG [container element](/en-US/docs/Web/SVG/Reference/Element#container_elements) or [graphics element](/en-US/docs/Web/SVG/Reference/Element#graphics_elements).

Text in a `<title>` element is not rendered as part of the graphic, but browsers usually display it as a tooltip. If an element can be described by visible text, it is recommended to reference that text with an [`aria-labelledby`](/en-US/docs/Web/Accessibility/ARIA/Reference/Attributes/aria-labelledby) attribute rather than using the `<title>` element.

> [!NOTE]
> For backward compatibility with SVG 1.1, `<title>` elements should be the first child element of their parent.

## Usage context

{{svginfo}}

## Attributes

This element only includes global attributes.

## DOM Interface

This element implements the {{domxref("SVGTitleElement")}} interface.

## Example

```css hidden
html,
body,
svg {
  height: 100%;
}
```

```html
<svg viewBox="0 0 20 10" xmlns="http://www.w3.org/2000/svg">
  <circle cx="5" cy="5" r="4">
    <title>I'm a circle</title>
  </circle>

  <rect x="11" y="1" width="8" height="8">
    <title>I'm a square</title>
  </rect>
</svg>
```

{{EmbedLiveSample('Example', 150, '100%')}}

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- {{SVGElement("desc")}}
