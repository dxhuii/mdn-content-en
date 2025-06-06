---
title: "ARIA: aria-describedby attribute"
short-title: aria-describedby
slug: Web/Accessibility/ARIA/Reference/Attributes/aria-describedby
page-type: aria-attribute
spec-urls: https://w3c.github.io/aria/#aria-describedby
sidebar: accessibilitysidebar
---

The global `aria-describedby` attribute identifies the element (or elements) that describes the element on which the attribute is set.

## Description

The `aria-describedby` attribute lists the [`id`](/en-US/docs/Web/HTML/Reference/Global_attributes/id)s of the elements that describe the object. It is used to establish a relationship between widgets or groups and the text that describes them.

The `aria-describedby` attribute is not limited to form controls. It can also be used to associate static text with widgets, groups of elements, regions that have a heading, definitions, and more. The `aria-describedby` attribute can be used with semantic HTML elements and with elements that have an ARIA [`role`](/en-US/docs/Web/Accessibility/ARIA/Reference/Roles).

The `aria-describedby` attribute is very similar to the [`aria-labelledby`](/en-US/docs/Web/Accessibility/ARIA/Reference/Attributes/aria-labelledby) attribute. While `aria-labelledby` lists the `id`s of the labels or elements that describe the essence of an object, `aria-describedby` lists the `id`s of the descriptions or elements providing more information that the user might need. Both `aria-labelledby` and `aria-describedby` reference other elements to calculate a text alternative, but a label should be concise, while a description is intended to provide more verbose information; a label describes the essence of an object, while a description provides more information that the user might need.

The elements linked via `aria-describedby` don't need to be visible. It is possible to reference an element even if that element is hidden. For example, a form control can have a description that is hidden by default and revealed on request using a disclosure widget like a "more information" icon. The sighted users click on the icon to view the description, while assistive technology users can immediately access it as the description is referenced from that form control with `aria-describedby`.

The `aria-describedby` property is appropriate when the associated content contains plain text. If the content is extensive, contains useful semantics, or has a complex structure requiring user navigation, use [`aria-details`](/en-US/docs/Web/Accessibility/ARIA/Reference/Attributes/aria-details) instead. `aria-details` allows assistive technology users to visit the associated structured content and provides additional navigation commands, making it easier to understand the structure, or to experience the information in smaller pieces.

> [!NOTE]
> The `aria-describedby` content should only be a text string. If there are important underlying semantics in the content, consider using [`aria-details`](/en-US/docs/Web/Accessibility/ARIA/Reference/Attributes/aria-details).

## Example

```html
<button aria-describedby="trash-desc">Move to trash</button>
…
<p id="trash-desc">
  Items in the trash will be permanently removed after 30 days.
</p>
```

> [!NOTE]
> The `aria-describedby` attribute is not designed to reference descriptions from external resources. As its value is one or more `id`s (space-separated if multiple), it must reference elements in the same DOM document.

## Values

- ID reference list
  - : The `id` or space-separated list of element `id`s that describe the current element.

## Associated interfaces

- {{domxref("Element.ariaDescribedByElements")}}
  - : The `ariaDescribedByElements` property is part of each element's interface.
    Its value is an array of subclasses of {{domxref("Element")}} that reflect the `id` references in the `aria-describedby` attribute ([with some caveats](/en-US/docs/Web/API/Document_Object_Model/Reflected_attributes#reflected_element_references)).
- {{domxref("ElementInternals.ariaDescribedByElements")}}
  - : The `ariaDescribedByElements` property is part of each custom element's interface.
    Its value is an array of subclasses of {{domxref("Element")}} that reflect the `id` references in the `aria-describedby` attribute ([with some caveats](/en-US/docs/Web/API/Document_Object_Model/Reflected_attributes#reflected_element_references)).

## Associated roles

Used in **all** roles. Usable in all HTML elements as well.

## Specifications

{{Specifications}}

## See also

- [`aria-labelledby`](/en-US/docs/Web/Accessibility/ARIA/Reference/Attributes/aria-labelledby)
- [`aria-description`](/en-US/docs/Web/Accessibility/ARIA/Reference/Attributes/aria-description)
- [`aria-details`](/en-US/docs/Web/Accessibility/ARIA/Reference/Attributes/aria-details)
- [Browser and AT support for `aria-describedby`](https://a11ysupport.io/tech/aria/aria-describedby_attribute)
