# 03. Initial, animate, exit, and keyframes

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Motion components and animation values](./02-motion-components-and-animation-values.md) | [Notes index](../README.md) | [Next: Transitions, easing, and springs](./04-transitions-easing-and-springs.md) |

## Describe the states of an element

initial is the starting target for an entering motion component. animate is the target it moves toward. When animate changes, Motion transitions from the current value to the new target.

~~~jsx
import { motion } from "motion/react";

export function WelcomeMessage() {
  return (
    <motion.p
      initial={{ opacity: 0, y: 10 }}
      animate={{ opacity: 1, y: 0 }}
    >
      Settings saved
    </motion.p>
  );
}
~~~

The paragraph begins slightly lower and transparent, then reaches its normal position and becomes visible. Keep the distance small so the movement supports the message rather than distracting from it.

Set initial={false} when an element should appear immediately at its animate values instead of playing an entrance animation. This is useful for content that should not animate on first display.

## Animate through keyframes

An array in an animate value defines keyframes. Motion moves through them in order.

~~~jsx
<motion.div
  initial={{ opacity: 0, x: 0 }}
  animate={{
    opacity: [0, 1, 1],
    x: [0, 12, 0],
  }}
  transition={{
    duration: 0.7,
    times: [0, 0.35, 1],
    repeat: 1,
    repeatType: "reverse",
  }}
/>
~~~

times sets the point in the transition where each keyframe occurs. It must use values between zero and one and have a value for each keyframe. Without a times array, Motion distributes the keyframes across the transition.

Use a small number of keyframes with clear meaning. Many arbitrary points are harder to tune and can make the motion feel mechanical.

## Respond to a changing target

A React state can select one of several targets.

~~~jsx
import { useState } from "react";
import { motion } from "motion/react";

export function ExpandableSummary() {
  const [expanded, setExpanded] = useState(false);

  return (
    <section>
      <button
        type="button"
        aria-expanded={expanded}
        onClick={() => setExpanded((value) => !value)}
      >
        {expanded ? "Show less" : "Show more"}
      </button>

      <motion.div
        animate={{
          opacity: expanded ? 1 : 0.7,
          scale: expanded ? 1 : 0.98,
        }}
      >
        Summary details
      </motion.div>
    </section>
  );
}
~~~

The button controls the real expanded state. The animation only reflects it visually. For content that is actually added or removed from the DOM, use an exit-presence pattern rather than hiding important content only with opacity.

## Use exit when a component leaves React

React removes a component immediately when a conditional becomes false. AnimatePresence keeps a removed child rendered long enough for its exit target to finish.

~~~jsx
import { useState } from "react";
import { AnimatePresence, motion } from "motion/react";

export function DetailsPanel() {
  const [visible, setVisible] = useState(true);

  return (
    <section>
      <button
        type="button"
        onClick={() => setVisible((value) => !value)}
      >
        Toggle details
      </button>

      <AnimatePresence>
        {visible ? (
          <motion.aside
            key="details"
            initial={{ opacity: 0, x: 12 }}
            animate={{ opacity: 1, x: 0 }}
            exit={{ opacity: 0, x: -12 }}
          >
            Extra details
          </motion.aside>
        ) : null}
      </AnimatePresence>
    </section>
  );
}
~~~

The direct child needs a stable, unique key so AnimatePresence can tell which item was removed. The next chapters cover transition control and exit behavior in more detail.

## Practice questions

1. What does initial describe?
2. What does animate describe?
3. What happens when an animate target changes?
4. How does initial={false} change the first render?
5. How are keyframes represented in an animate target?
6. What does times control?
7. Why should UI state remain separate from its visual animation?
8. What does AnimatePresence do for a removed component?

## Main references

- [Motion component animation props](https://motion.dev/docs/react-motion-component)
- [Keyframes and transitions](https://motion.dev/docs/react-transitions)
- [AnimatePresence](https://motion.dev/docs/react-animate-presence)
- [React animation overview](https://motion.dev/docs/react-animation)
