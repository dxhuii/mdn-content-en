---
title: "Window: devicemotion event"
short-title: devicemotion
slug: Web/API/Window/devicemotion_event
page-type: web-api-event
browser-compat: api.Window.devicemotion_event
---

{{APIRef("Device Orientation Events")}}{{securecontext_header}}

The **`devicemotion`** event is fired at a regular interval and indicates the acceleration rate of the device with/without the contribution of the gravity force at that time. It also provides information about the rate of rotation, if available.

This event is not cancelable and does not bubble.

## Syntax

Use the event name in methods like {{domxref("EventTarget.addEventListener", "addEventListener()")}}, or set an event handler property.

```js-nolint
addEventListener("devicemotion", (event) => { })

ondevicemotion = (event) => { }
```

## Event type

A {{domxref("DeviceMotionEvent")}}. Inherits from {{domxref("Event")}}.

{{InheritanceDiagram("DeviceMotionEvent")}}

## Event properties

- {{DOMxRef("DeviceMotionEvent.acceleration")}} {{ReadOnlyInline}}
  - : An object giving the acceleration of the device on the three axis: x, y, and z. Acceleration is expressed in [m/s²](https://en.wikipedia.org/wiki/Meter_per_second_squared).
- {{DOMxRef("DeviceMotionEvent.accelerationIncludingGravity")}} {{ReadOnlyInline}}
  - : An object giving the acceleration of the device on the three axis: x, y, and z with the effect of gravity. Acceleration is expressed in [m/s²](https://en.wikipedia.org/wiki/Meter_per_second_squared).
- {{DOMxRef("DeviceMotionEvent.rotationRate")}} {{ReadOnlyInline}}
  - : An object giving the rate of change of the device's orientation on the three orientation axis: alpha, beta and gamma. Rotation rate is expressed in degrees per seconds.
- {{DOMxRef("DeviceMotionEvent.interval")}} {{ReadOnlyInline}}
  - : A number representing the interval of time, in milliseconds, at which data is obtained from the device.

## Examples

```js
function handleMotionEvent(event) {
  const x = event.accelerationIncludingGravity.x;
  const y = event.accelerationIncludingGravity.y;
  const z = event.accelerationIncludingGravity.z;

  // Do something awesome.
}

window.addEventListener("devicemotion", handleMotionEvent, true);
```

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- {{domxref("Window.deviceorientation_event", "deviceorientation")}}
