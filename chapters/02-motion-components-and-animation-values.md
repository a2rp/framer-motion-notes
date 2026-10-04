# 02. Motion components and animation values

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Motion for React setup and first animation](./01-motion-for-react-setup-and-first-animation.md) | [Notes index](../README.md) | [Next: Initial, animate, exit, and keyframes](./03-initial-animate-exit-and-keyframes.md) |

## Start with the right motion element

Motion provides a component for each HTML and SVG element. Use motion.div for a div, motion.button for a button, and motion.circle for an SVG circle. The element keeps its normal attributes and accepts Motion props such as animate, whileHover, and layout.

~~~jsx
import { motion } from "motion/react";

export function MotionExamples() {
  return (
    <div>
      <motion.button
        type="button"
        whileHover={{ scale: 1.04 }}
        whileTap={{ scale: 0.97 }}
      >
        Add item
      </motion.button>

      <motion.svg viewBox="0 0 100 40" aria-label="Progress">
        <motion.circle
          cx="20"
          cy="20"
          r="8"
          animate={{ cx: 80 }}
          transition={{ duration: 0.5 }}
        />
      </motion.svg>
    </div>
  );
}
~~~

Use semantic HTML elements for their meaning. A motion.button is still a button, so it can be focused and activated by a keyboard. A motion.div is still a generic container, so do not use it in place of a button or link.

## Keep normal styles and animation separate

A motion component accepts className and style like a normal React element. Use CSS for layout, colors, and static presentation. Use Motion props for values that should change over time or in response to interaction.

~~~jsx
<motion.article
  className="card"
  initial={{ opacity: 0, y: 12 }}
  animate={{ opacity: 1, y: 0 }}
  whileHover={{ y: -3 }}
  style={{ borderRadius: 12 }}
>
  <h2>Project summary</h2>
  <p>Three open tasks</p>
</motion.article>
~~~

Motion supports transform shorthand values such as x, y, scale, and rotate. These values are combined into a transform without manually building a CSS transform string.

~~~jsx
<motion.div
  animate={{ x: 24, rotate: 2, scale: 1.02 }}
  transition={{ duration: 0.2 }}
/>
~~~

Prefer transform and opacity for frequent movement when they express the intended effect. Properties such as width, height, and layout can be useful, but may cause more browser layout work.

## Add motion to a custom component

A custom component must provide Motion with a real DOM element to animate. It needs to forward a ref and apply the style prop to that same element.

~~~jsx
import { forwardRef } from "react";
import { motion } from "motion/react";

const BaseButton = forwardRef(function BaseButton(
  { style, ...props },
  ref
) {
  return <button ref={ref} style={style} {...props} />;
});

const MotionButton = motion.create(BaseButton);

export function CustomButton() {
  return (
    <MotionButton
      type="button"
      whileHover={{ scale: 1.03 }}
      style={{ borderRadius: 10 }}
    >
      Continue
    </MotionButton>
  );
}
~~~

Create the Motion component outside the React render function. Creating it during each render makes React see a different component identity and can reset the animation or component state.

If a third-party component cannot forward a ref or apply styles to its underlying element, animate a wrapper you control.

## Practice questions

1. Which motion component should be used for a semantic button?
2. Can a motion component render an SVG element?
3. Which usual React styling props can a motion component receive?
4. What do x, y, scale, and rotate represent?
5. Why should semantic HTML be preserved in animated interfaces?
6. What must a custom component provide so Motion can animate it?
7. Where should motion.create be called?
8. Which values are often suitable for frequent visual movement?

## Main references

- [Motion component](https://motion.dev/docs/react-motion-component)
- [Motion for React installation](https://motion.dev/docs/react-installation)
- [Motion values overview](https://motion.dev/docs/react-motion-value)
- [Custom component troubleshooting](https://motion.dev/troubleshooting/custom-component-ref)
