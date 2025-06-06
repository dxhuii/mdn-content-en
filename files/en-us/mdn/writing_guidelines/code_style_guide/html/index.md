---
title: Guidelines for writing HTML code examples
short-title: HTML examples
slug: MDN/Writing_guidelines/Code_style_guide/HTML
page-type: mdn-writing-guide
sidebar: mdnsidebar
---

The following guidelines cover how to write HTML example code for MDN Web Docs.

## General guidelines for HTML code examples

### Choosing a format

Opinions on correct indentation, whitespace, and line lengths have always been controversial. Discussions on these topics are a distraction from creating and maintaining content.

On MDN Web Docs, we use [Prettier](https://prettier.io/) as a code formatter to keep the code style consistent (and to avoid off-topic discussions). You can consult our [configuration file](https://github.com/mdn/content/blob/main/.prettierrc.json) to learn about the current rules, and read the [Prettier documentation](https://prettier.io/docs/index.html).

Prettier formats all the code and keeps the style consistent. Nevertheless, there are a few additional rules that you need to follow.

## Complete HTML document

> [!NOTE]
> The guidelines in this section apply only when you need to show a complete HTML document. A snippet is usually enough to demonstrate a feature. When using the [EmbedLiveSample macro](/en-US/docs/MDN/Writing_guidelines/Page_structures/Code_examples#live_samples), just include the HTML snippet; it will automatically be inserted into a full HTML document when displayed.

### Doctype

You should use the HTML5 {{Glossary("Doctype", "doctype")}}.

```html example-good
<!doctype html>
```

### Document language

Set the document language using the [`lang`](/en-US/docs/Web/HTML/Reference/Global_attributes/lang) attribute on your {{htmlelement("html")}} element:

```html example-good
<html lang="en-US"></html>
```

This is good for accessibility and search engines, helps with localizing content, and reminds people to use best practices.

### Document character set

You should also define your document's character set like so:

```html example-good
<meta charset="utf-8" />
```

Use UTF-8 unless you have a very good reason not to; it will cover all character needs pretty much regardless of what language you are using in your document.

### Viewport meta tag

Finally, you should always add the viewport meta tag into your HTML {{HTMLElement("head")}} to give the code example a better chance of working on mobile devices. You should include at least the following in your document, which can be modified later on as the need arises:

```html example-good
<meta name="viewport" content="width=device-width" />
```

See [Using the viewport meta tag to control layout on mobile browsers](/en-US/docs/Web/HTML/Guides/Viewport_meta_element) for further details.

## Attributes

You should put all attribute values in double quotes. It is tempting to omit quotes since HTML5 allows this, but markup is neater and easier to read if you do include them. For example, this is better:

```html example-good
<img src="images/logo.jpg" alt="A circular globe icon" class="no-border" />
```

…than this:

```html-nolint example-bad
<img src=images/logo.jpg alt=A circular globe icon class=no-border>
```

Omitting quotes can also cause problems. In the above example, the `alt` attribute will be interpreted as multiple attributes because there are no quotes to specify that "A circular globe icon" is a single attribute value.

## Boolean attributes

Don't include values for boolean attributes (but do include values for {{glossary("enumerated")}} attributes); you can just write the attribute name to set it. For example, you can write:

```html example-good
<input required />
```

This is perfectly understandable and works fine. If a boolean HTML attribute is present, the value is true. While including a value will work, it is not necessary and incorrect:

```html example-bad
<input required="required" />
```

## Casing convention on MDN

Use lowercase for all case-insensitive constructs, including the doctype declaration, element names, and attribute names/values. This creates a consistent appearance and allows for faster markup writing.

```html example-good
<p class="nice">This looks nice and neat</p>
```

```html-nolint example-bad
<P CLASS="WHOA-THERE">Why is my markup shouting?</P>
```

## Class and ID names

Use semantic class/ID names, and separate multiple words with hyphens ({{Glossary("kebab_case", "kebab case")}}). Don't use {{Glossary("camel_case", "camel case")}}. For example:

```html example-good
<p class="editorial-summary">Blah blah blah</p>
```

```html example-bad
<p class="bigRedBox">Blah blah blah</p>
```

## Character references

Don't use {{glossary("character reference", "character references")}} unnecessarily — use the literal character wherever possible (you'll still need to escape characters like angle brackets and quote marks).

As an example, you could just write:

```html example-good
<p>© 2018 Me</p>
```

Instead of:

```html example-bad
<p>&copy; 2018 Me</p>
```

## HTML elements

There are some rules for writing about HTML elements on MDN Web Docs. Adhering to these rules produces consistent descriptions of elements and their components and also ensures correct linking to detailed documentation.

- **Element names**: Use the [`HTMLElement`](https://github.com/mdn/rari/blob/main/crates/rari-doc/src/templ/templs/links/htmlxref.rs) macro, which creates a link to the MDN Web Docs page for that element. For example, writing `\{{HTMLElement("title")}}` produces "{{HTMLElement("title")}}".
  If you don't want to create a link, **enclose the name in angle brackets** and use the "Inline Code" style (e.g., `<title>`).
- **Attribute names**: Use "Inline Code" style to put attribute names in `code font`.
  Additionally, put them in **`bold face`** when the attribute is mentioned in association with an explanation of what it does or when it is used for the first time on the page.
- **Attribute values**: Use the "Inline Code" style to apply `<code>` to attribute values, and don't use quotation marks around string values, unless needed by the syntax of a code sample. For example, "When the `type` attribute of an `<input>` element is set to `email` or `tel` ...".
