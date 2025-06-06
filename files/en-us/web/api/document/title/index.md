---
title: "Document: title property"
short-title: title
slug: Web/API/Document/title
page-type: web-api-instance-property
browser-compat: api.Document.title
---

{{APIRef("DOM")}}

The **`document.title`** property gets or sets the current title of the document.
When present, it defaults to the value of the [`<title>`](/en-US/docs/Web/HTML/Reference/Elements/title).

## Value

A string containing the _document_'s title. If the title was overridden by setting `document.title`, it contains that value. Otherwise, it contains the title specified in the [`<title>`](/en-US/docs/Web/HTML/Reference/Elements/title) element.

```js
document.title = newTitle;
```

`newTitle` is the new title of the document. The assignment
affects the return value of `document.title`, the title displayed for the
document (e.g., in the titlebar of the window or tab), and it also affects the DOM of the
document (e.g., the content of the `<title>` element in an HTML
document).

## Examples

Assume the document's `<head>` looks like:

```html
<head>
  <meta charset="UTF-8" />
  <title>Hello World!</title>
</head>
```

```js
console.log(document.title); // "Hello World!"
document.title = "Goodbye World!"; // Page title changed
console.log(document.title); // "Goodbye World!"
```

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}
