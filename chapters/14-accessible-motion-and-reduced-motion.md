# 14. Accessible motion and reduced motion

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: SVG and path animation](./13-svg-and-path-animation.md) | [Notes index](../README.md) | [Next: React patterns and bundle choices](./15-react-patterns-and-bundle-choices.md) |

## Respect the operating system preference

Some users prefer less motion because movement can cause discomfort or make content harder to follow. MotionConfig with reducedMotion="user" applies the user's reduced-motion preference across its child motion components.

~~~jsx
import { MotionConfig, motion } from "motion/react";

export function AppMotion() {
  return (
    <MotionConfig reducedMotion="user">
      <motion.main
        initial={{ opacity: 0, y: 16 }}
        animate={{ opacity: 1, y: 0 }}
      >
        <h1>Study notes</h1>
        <p>The content remains available while the entrance effect runs.</p>
      </motion.main>
    </MotionConfig>
  );
}
~~~

When reduced motion is preferred, Motion disables transform and layout animations while opacity and color animations can continue. This is a useful baseline, but review each interaction. A long fade, repeated pulse, or flashing color may still be uncomfortable.

## Choose a reduced alternative with useReducedMotion

Use the hook when the interaction needs a different animation for users who prefer reduced motion.

~~~jsx
import { motion, useReducedMotion } from "motion/react";

export function MotionAwareNotice() {
  const shouldReduceMotion = useReducedMotion();

  return (
    <motion.aside
      initial={shouldReduceMotion ? { opacity: 0 } : { opacity: 0, y: 24 }}
      animate={{ opacity: 1, y: 0 }}
      transition={{
        duration: shouldReduceMotion ? 0.15 : 0.4,
      }}
      style={{ padding: 20, border: "1px solid #888" }}
    >
      <h2>Saved</h2>
      <p>Your notes are available in the list.</p>
    </motion.aside>
  );
}
~~~

The reduced version fades without traveling across the screen. For some effects, the right reduced alternative is to remove the animation altogether. The message still appears in the document and does not depend on motion to be understood.

## Keep interaction and focus accessible

Use semantic controls such as button and a. Motion changes their visual behavior; it does not add keyboard behavior or accessible names.

~~~jsx
import { motion } from "motion/react";

export function SaveButton({ onSave }) {
  return (
    <motion.button
      type="button"
      onClick={onSave}
      whileHover={{ y: -1 }}
      whileTap={{ scale: 0.98 }}
      whileFocus={{ outline: "2px solid #e85b24", outlineOffset: 3 }}
    >
      Save notes
    </motion.button>
  );
}
~~~

Do not remove the browser focus indicator unless you replace it with a visible alternative. Confirm that focus remains visible while an element is animated, and that hover is not the only way to discover an action. Respect touch input and avoid requiring dragging to complete an important task.

## Review timing and motion intensity

Keep movement small, predictable, and connected to the user action. Avoid rapidly flashing or looping effects, large parallax movement, and animations that delay access to important information.

A useful review checks whether content remains readable, whether controls work with keyboard and touch, whether focus is visible, and whether the reduced-motion setting changes the most noticeable movement. Keep the animation short enough that the interface does not feel blocked.

## Practice questions

1. What does reducedMotion="user" read?
2. Which animation types does Motion disable by default under reduced motion?
3. Why should every interaction still be reviewed after setting MotionConfig?
4. What does useReducedMotion return?
5. When might removing an animation be better than replacing it with a fade?
6. Why do semantic buttons remain necessary for animated controls?
7. What should replace a removed browser focus indicator?
8. Which movement patterns can make content uncomfortable or difficult to follow?

## Main references

- [Accessibility and reduced motion](https://motion.dev/docs/react-accessibility)
- [MotionConfig](https://motion.dev/docs/react-motion-config)
- [useReducedMotion](https://motion.dev/docs/react-use-reduced-motion)
- [Gesture animations](https://motion.dev/docs/react-gestures)