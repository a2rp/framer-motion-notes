# 13. SVG and path animation

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Sequences and imperative control](./12-sequences-and-imperative-control.md) | [Notes index](../README.md) | [Next: Accessible motion and reduced motion](./14-accessible-motion-and-reduced-motion.md) |

## Animate SVG attributes

Motion provides SVG elements such as motion.svg, motion.path, motion.circle, and motion.rect. Their animation props can target SVG attributes as well as style values.

~~~jsx
import { motion } from "motion/react";

export function AnimatedDot() {
  return (
    <motion.svg
      viewBox="0 0 120 60"
      role="img"
      aria-labelledby="dot-title"
      style={{ width: 240, overflow: "visible" }}
    >
      <title id="dot-title">A dot moving along a line</title>
      <line x1="10" y1="30" x2="110" y2="30" stroke="#888" strokeWidth="2" />
      <motion.circle
        cx="10"
        cy="30"
        r="8"
        fill="#e85b24"
        animate={{ cx: 110 }}
        transition={{ duration: 1.2, repeat: Infinity, repeatType: "reverse" }}
      />
    </motion.svg>
  );
}
~~~

SVG coordinates come from the viewBox, not CSS pixels. The browser scales the viewBox into the rendered width. Keep the coordinate system and shape dimensions easy to understand before adjusting responsive sizing.

## Draw a path

Motion can animate the normalized pathLength value from zero to one. This creates a path drawing effect when the SVG path has a visible stroke.

~~~jsx
import { motion } from "motion/react";

export function Checkmark() {
  return (
    <motion.svg
      viewBox="0 0 48 48"
      role="img"
      aria-labelledby="check-title"
      style={{ width: 96, height: 96 }}
    >
      <title id="check-title">Completed</title>
      <motion.path
        d="M8 25 L19 36 L40 11"
        fill="none"
        stroke="#e85b24"
        strokeWidth="4"
        strokeLinecap="round"
        strokeLinejoin="round"
        initial={{ pathLength: 0 }}
        animate={{ pathLength: 1 }}
        transition={{ duration: 0.65, ease: "easeInOut" }}
      />
    </motion.svg>
  );
}
~~~

pathLength is a normalized drawing value. The actual path can be any length. A visible stroke is needed for the drawing effect. Use fill="none" when the path should be an outline.

## Sequence several SVG strokes

Use variants to coordinate several path children. The parent controls when the paths begin, while each child describes its own drawing animation.

~~~jsx
import { motion } from "motion/react";

const drawing = {
  hidden: {},
  visible: {
    transition: { staggerChildren: 0.18 },
  },
};

const stroke = {
  hidden: { pathLength: 0, opacity: 0.4 },
  visible: { pathLength: 1, opacity: 1 },
};

export function SimpleMark() {
  return (
    <motion.svg
      viewBox="0 0 100 60"
      initial="hidden"
      animate="visible"
      variants={drawing}
      role="img"
      aria-label="Three orange strokes"
      style={{ width: 200 }}
    >
      <motion.path
        d="M10 50 L30 10"
        stroke="#e85b24"
        strokeWidth="5"
        variants={stroke}
      />
      <motion.path
        d="M40 50 L60 10"
        stroke="#e85b24"
        strokeWidth="5"
        variants={stroke}
      />
      <motion.path
        d="M70 50 L90 10"
        stroke="#e85b24"
        strokeWidth="5"
        variants={stroke}
      />
    </motion.svg>
  );
}
~~~

For a decorative SVG that adds no information, hide it from assistive technology with aria-hidden="true". For an informative SVG, provide a title or a clear accessible name. Do not rely on animation alone to communicate success, failure, or progress.

## Keep SVG motion clear

Path morphing between two d values depends on compatible path structures. If the shape commands do not correspond, interpolation may not produce the expected result. For unrelated shapes, animate opacity or position, or crossfade between separate paths instead.

Use SVG animation for focused feedback such as a check mark, diagram state, or small illustration. Repeating motion should have a clear purpose and a way to stop or pause when it could distract.

## Practice questions

1. Which SVG elements have Motion component versions?
2. What does the SVG viewBox describe?
3. What produces a path drawing effect?
4. Why does a path drawing example need a stroke?
5. How can variants sequence multiple SVG paths?
6. How should a decorative SVG be exposed to assistive technology?
7. Why can path morphing fail between unrelated d values?
8. What should be considered before repeating an SVG animation?

## Main references

- [SVG animation](https://motion.dev/docs/react-svg-animation)
- [Motion component](https://motion.dev/docs/react-motion-component)
- [Variants](https://motion.dev/docs/react-variants)
- [Accessibility and reduced motion](https://motion.dev/docs/react-accessibility)