# 04. Transitions, easing, and springs

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Initial, animate, exit, and keyframes](./03-initial-animate-exit-and-keyframes.md) | [Notes index](../README.md) | [Next: Variants and animation orchestration](./05-variants-and-animation-orchestration.md) |

## What a transition controls

A transition decides how an animated value moves to its target. It can set duration, easing, delay, repeat behavior, and the animation type.

A tween follows a duration and an easing curve. It works well when movement must finish at a predictable time, such as fading a notification or moving a panel into view.

~~~jsx
<motion.div
  initial={{ opacity: 0, y: 12 }}
  animate={{ opacity: 1, y: 0 }}
  transition={{
    type: "tween",
    duration: 0.24,
    ease: "easeOut",
  }}
/>
~~~

A duration is measured in seconds. Common easing names include linear, easeIn, easeOut, and easeInOut. easeOut starts quickly and settles toward the target, which often feels natural for an element arriving on screen.

## Shape a spring

A spring is controlled by physical values rather than a fixed timeline. stiffness controls how strongly it moves toward the target. damping controls how much oscillation is removed. mass changes how heavy the movement feels.

~~~jsx
<motion.button
  whileTap={{ scale: 0.96 }}
  transition={{
    type: "spring",
    stiffness: 380,
    damping: 24,
  }}
>
  Add to list
</motion.button>
~~~

Higher stiffness makes a spring respond more sharply. Higher damping reduces bouncing. Tune one value at a time and observe how the interaction feels at its real size.

A spring can also use duration and bounce when a predictable overall timing is easier to tune.

~~~jsx
<motion.div
  animate={{ scale: 1 }}
  transition={{
    type: "spring",
    duration: 0.35,
    bounce: 0.18,
  }}
/>
~~~

Do not set duration and bounce together with stiffness, damping, or mass and expect each setting to remain independent. The physical spring settings determine a different behavior.

## Give different values different transitions

One element can animate its position with a spring and opacity with a tween.

~~~jsx
<motion.aside
  animate={{ x: 0, opacity: 1 }}
  transition={{
    default: { type: "spring", stiffness: 260, damping: 28 },
    opacity: { type: "tween", duration: 0.2 },
  }}
/>
~~~

Use value-specific transitions only when the values need noticeably different behavior. One shared transition is easier to understand and maintain.

## Delay and repeat intentionally

delay postpones an animation. repeat sets how many additional times it plays. repeatType can loop, reverse, or mirror the animation.

~~~jsx
<motion.span
  animate={{ rotate: 360 }}
  transition={{
    duration: 1.2,
    ease: "linear",
    repeat: Infinity,
  }}
  aria-hidden="true"
/>
~~~

Continuous movement should have a clear purpose and should respect reduced motion. Avoid looping decorative motion beside important text or controls.

## Set a shared default

MotionConfig can provide a default transition for descendants. A component can still use a more specific transition when a particular value needs different behavior.

~~~jsx
import { MotionConfig, motion } from "motion/react";

export function App() {
  return (
    <MotionConfig transition={{ duration: 0.22, ease: "easeOut" }}>
      <motion.main animate={{ opacity: 1 }}>
        Application content
      </motion.main>
    </MotionConfig>
  );
}
~~~

Set a shared default only when the same motion style makes sense across the group. Avoid placing a global transition around unrelated interactions just to reduce a few repeated lines.

## Practice questions

1. What does a transition configure?
2. When is a tween useful?
3. What does easeOut do?
4. What does spring stiffness control?
5. How does damping affect a spring?
6. When can a duration-based spring be useful?
7. How can position and opacity use different transitions?
8. What should be considered before using an infinite repeat?

## Main references

- [Motion transitions](https://motion.dev/docs/react-transitions)
- [React animation overview](https://motion.dev/docs/react-animation)
- [MotionConfig component](https://motion.dev/docs/react-motion-config)
- [Accessible motion](https://motion.dev/docs/react-accessibility)
