---
title: "Screen: orientationchange event"
short-title: orientationchange
slug: Web/API/Screen/orientationchange_event
page-type: web-api-event
status:
  - deprecated
  - non-standard
browser-compat: api.Screen.orientationchange_event
---

{{APIRef("Screen Orientation API")}}{{Deprecated_Header}}{{Non-standard_Header}}

The `orientationchange` event fires when the device's orientation has changed.

## Syntax

Use the event name in methods like {{domxref("EventTarget.addEventListener", "addEventListener()")}}, or set an event handler property.

```js-nolint
addEventListener("orientationchange", (event) => { })

onorientationchange = (event) => { }
```

## Event type

A generic {{domxref("Event")}}.

## Specifications

This feature is not part of any specification. It is no longer on track to becoming a standard.

Use the `ScreenOrientation` {{domxref("ScreenOrientation.change_event", "change")}} event instead.

## Browser compatibility

{{Compat}}

## See also

- [Managing screen orientation](/en-US/docs/Web/API/CSS_Object_Model/Managing_screen_orientation)
