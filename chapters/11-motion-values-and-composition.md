# 11. Motion values and composition

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Scroll-linked animation](./10-scroll-linked-animation.md) | [Notes index](../README.md) | [Next: Sequences and imperative control](./12-sequences-and-imperative-control.md) |

## Store a visual value with useMotionValue

A Motion value stores a value and notifies Motion when it changes. Passing it to a motion component style lets the element update without React rendering again for every visual update.

~~~jsx
import { useMotionValue, motion } from "motion/react";

export function PointerFollower() {
  const x = useMotionValue(0);
  const y = useMotionValue(0);

  function movePointer(event) {
    x.set(event.clientX);
    y.set(event.clientY);
  }

  return (
    <div
      onPointerMove={movePointer}
      style={{ height: 240, border: "1px solid #888", position: "relative" }}
    >
      <motion.div
        style={{
          x,
          y,
          width: 24,
          height: 24,
          borderRadius: "50%",
          background: "#e85b24",
          position: "absolute",
          top: 0,
          left: 0,
          pointerEvents: "none",
        }}
      />
      Move your pointer inside this area
    </div>
  );
}
~~~

The element follows the pointer relative to the page because clientX and clientY are viewport coordinates. For a follower constrained to the panel, subtract the panel's bounding rectangle from the pointer coordinates. Also consider touch, pointer cancellation, and reduced motion before using this effect in a real interface.

## Derive values with useTransform

useTransform creates a value from another Motion value. Use it to map a range or derive a string for a visual property.

~~~jsx
import { motion, useMotionValue, useTransform } from "motion/react";

export function TiltCard() {
  const pointerX = useMotionValue(0);
  const rotate = useTransform(pointerX, [-0.5, 0.5], [-7, 7]);

  function updatePointer(event) {
    const bounds = event.currentTarget.getBoundingClientRect();
    const normalizedX = (event.clientX - bounds.left) / bounds.width - 0.5;
    pointerX.set(normalizedX);
  }

  return (
    <motion.div
      onPointerMove={updatePointer}
      onPointerLeave={() => pointerX.set(0)}
      style={{ rotate, padding: 24, border: "1px solid #888" }}
    >
      Move across this card
    </motion.div>
  );
}
~~~

The source range and output range make the mapping visible: the pointer position moves from about -0.5 to 0.5, and rotation moves from -7 to 7 degrees. Reset the source value when the pointer leaves so the card returns to its neutral position.

## Smooth a value with useSpring

useSpring can follow another Motion value with spring physics. It is useful when direct tracking feels too sharp.

~~~jsx
import { motion, useMotionValue, useSpring } from "motion/react";

export function SmoothFollower() {
  const sourceX = useMotionValue(0);
  const x = useSpring(sourceX, { stiffness: 220, damping: 24 });

  return (
    <motion.div
      onPointerMove={(event) => sourceX.set(event.clientX)}
      style={{ x, padding: 16, border: "1px solid #888" }}
    >
      Move the pointer to see the spring follow
    </motion.div>
  );
}
~~~

A spring adds lag by design. Use it only when that movement helps the interaction. A control that must track the pointer exactly may be better without smoothing.

## Observe changes with useMotionValueEvent

useMotionValueEvent subscribes to a Motion value event and manages the subscription with the component lifecycle.

~~~jsx
import { useMotionValue, useMotionValueEvent } from "motion/react";

export function ValueObserver() {
  const x = useMotionValue(0);

  useMotionValueEvent(x, "change", (latest) => {
    if (latest > 200) {
      console.log("The value passed 200 pixels");
    }
  });

  return (
    <button type="button" onClick={() => x.set(x.get() + 50)}>
      Move value to {x.get()} pixels
    </button>
  );
}
~~~

The text in this sample reads the value during React rendering, so it changes only when this button causes a render. For a live readout, use a dedicated Motion component or update state only when the displayed value needs to change. Avoid setting React state on every animation frame.

## Compose instead of duplicating state

A Motion value can feed several derived values. For example, one scroll progress value can drive an indicator scale and a color mapping. Keep the source value as the single source of truth and derive visual outputs from it.

Do not use Motion values as a replacement for application state. They are suited to fast-changing visual values; React state remains a better fit for content and decisions that affect the component tree.

## Practice questions

1. What does useMotionValue create?
2. Why can Motion values update visuals without a React render for every frame?
3. How does useTransform derive an output from an input?
4. When can useSpring improve a Motion value?
5. What does useMotionValueEvent subscribe to?
6. Why might a live text readout still require React state?
7. Which values belong in Motion values and which belong in React state?
8. What should be considered before building a pointer-following effect?

## Main references

- [Motion values](https://motion.dev/docs/react-motion-value)
- [useMotionValue](https://motion.dev/docs/react-use-motion-value)
- [useTransform](https://motion.dev/docs/react-use-transform)
- [useSpring](https://motion.dev/docs/react-use-spring)
- [useMotionValueEvent](https://motion.dev/docs/react-use-motion-value-event)