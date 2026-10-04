# 06. Gestures, drag, and interaction states

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Variants and animation orchestration](./05-variants-and-animation-orchestration.md) | [Notes index](../README.md) | [Next: AnimatePresence and component exit](./07-animatepresence-and-component-exit.md) |

## Animate common gestures

Motion components can respond to hover, tap, focus, pan, drag, and viewport entry. The while props describe temporary visual targets while a gesture is active.

~~~jsx
import { motion } from "motion/react";

export function ActionButton() {
  return (
    <motion.button
      type="button"
      whileHover={{ y: -2 }}
      whileTap={{ scale: 0.97 }}
      whileFocus={{ outline: "2px solid #e85b24" }}
      transition={{ duration: 0.15 }}
    >
      Create note
    </motion.button>
  );
}
~~~

A button still needs a real action handler. Gesture animation gives feedback, but it does not replace application behavior or visible focus styling.

## Add a constrained drag surface

Use drag to let a user move an element with a pointer or touch input. A ref can define the boundary in which it may move.

~~~jsx
import { useRef } from "react";
import { motion } from "motion/react";

export function DragCard() {
  const boundaryRef = useRef(null);

  return (
    <div
      ref={boundaryRef}
      style={{
        width: 320,
        height: 180,
        border: "1px solid #aaa",
        position: "relative",
      }}
    >
      <motion.div
        drag
        dragConstraints={boundaryRef}
        dragElastic={0.08}
        dragMomentum={false}
        whileDrag={{ scale: 1.04 }}
        style={{
          width: 110,
          padding: 12,
          background: "#f0e6df",
          cursor: "grab",
        }}
      >
        Move this card
      </motion.div>
    </div>
  );
}
~~~

Use drag="x" or drag="y" to lock the movement to one axis. dragMomentum controls inertia after release. dragElastic controls how far the element may move beyond its constraints.

For a production draggable interface, provide clear boundaries and explain how to complete the same task without dragging. Drag should not be the only way to reorder or move important content.

## Handle pan gestures

Pan reports pointer movement information such as position, delta, offset, and velocity. Touch scrolling can compete with pan, so set touch-action on the gesture surface when the interaction requires pointer movement in a particular direction.

~~~jsx
import { motion } from "motion/react";

export function PanSurface() {
  function handlePan(event, info) {
    console.log(info.offset.x, info.offset.y);
  }

  return (
    <motion.div
      onPan={handlePan}
      style={{
        touchAction: "none",
        padding: 24,
        background: "#ececec",
      }}
    >
      Drag a pointer across this area
    </motion.div>
  );
}
~~~

Do not disable page scrolling across a large region without a clear need. If the interface only needs a vertical page scroll, keep native vertical scrolling available.

## Read gesture events

Callbacks such as onHoverStart, onTap, onPan, and onDragEnd let the application respond to an interaction. Use event callbacks for application logic and while props for visual feedback.

Avoid writing React state for every pointer movement. Fast-changing visual values can use Motion values, which are covered later.

## Practice questions

1. Which while props provide hover, tap, focus, and drag feedback?
2. Why should a motion button still have a real event handler?
3. How can drag be limited to one axis?
4. What does dragConstraints accept?
5. What is the difference between dragMomentum and dragElastic?
6. Which data does a pan callback receive?
7. Why can touch-action affect a pan gesture?
8. Why should dragging not be the only way to complete an important task?

## Main references

- [Gesture animations](https://motion.dev/docs/react-gestures)
- [Drag animation](https://motion.dev/docs/react-drag)
- [Motion component gesture props](https://motion.dev/docs/react-motion-component)
- [Accessibility](https://motion.dev/docs/react-accessibility)
