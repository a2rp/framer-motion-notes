# 10. Scroll-linked animation

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Viewport entry and in-view animation](./09-viewport-entry-and-in-view-animation.md) | [Notes index](../README.md) | [Next: Motion values and composition](./11-motion-values-and-composition.md) |

## Link a visual value to scroll progress

useScroll returns Motion values for scroll position and progress. Use useTransform to map progress to a visual property without setting React state on every scroll frame.

~~~jsx
import { useRef } from "react";
import { motion, useScroll, useSpring } from "motion/react";

export function ReadingProgress() {
  const articleRef = useRef(null);
  const { scrollYProgress } = useScroll({
    target: articleRef,
    offset: ["start start", "end end"],
  });
  const smoothProgress = useSpring(scrollYProgress, {
    stiffness: 100,
    damping: 30,
    restDelta: 0.001,
  });

  return (
    <article ref={articleRef} style={{ minHeight: "180vh", padding: 24 }}>
      <motion.div
        aria-hidden="true"
        style={{
          position: "fixed",
          top: 0,
          left: 0,
          right: 0,
          height: 4,
          scaleX: smoothProgress,
          transformOrigin: "0% 50%",
          background: "#e85b24",
        }}
      />
      <h1>Scroll through these notes</h1>
      <p>The progress line follows the article position.</p>
    </article>
  );
}
~~~

scrollYProgress is a Motion value between zero and one. The target option measures progress through an element. offset describes which points on the target and container mark the start and end of that progress range. The exact range should match the visual behavior you want.

Without target, useScroll tracks the page scroll position. To track a scrollable element, pass its ref as the container option. The returned scrollY is a pixel position, while scrollYProgress is normalized progress.

## Transform progress into another value

useTransform maps an input range to an output range. For example, map page progress to a heading's opacity and vertical position.

~~~jsx
import { motion, useTransform } from "motion/react";

function FadeWithScroll({ progress }) {
  const opacity = useTransform(progress, [0, 0.25, 0.7, 1], [0.3, 1, 1, 0.4]);
  const y = useTransform(progress, [0, 1], [40, -40]);

  return (
    <motion.h2 style={{ opacity, y }}>
      Scroll-linked heading
    </motion.h2>
  );
}
~~~

If you use the previous example as a standalone component, import motion in the same module as well. A Motion value can be passed as a style value directly. Keep the input and output ranges explicit so the effect is easy to inspect and adjust.

## Use a custom scroll container

The container must be scrollable and have a measurable size. Attach the ref to the element that owns scrolling.

~~~jsx
import { useRef } from "react";
import { motion, useScroll } from "motion/react";

export function ScrollPanel() {
  const panelRef = useRef(null);
  const { scrollYProgress } = useScroll({ container: panelRef });

  return (
    <div
      ref={panelRef}
      style={{ height: 280, overflowY: "auto", border: "1px solid #888" }}
    >
      <motion.div
        style={{
          scaleX: scrollYProgress,
          height: 4,
          background: "#e85b24",
          transformOrigin: "0% 50%",
        }}
      />
      <div style={{ minHeight: 700, padding: 20 }}>Scrollable panel content</div>
    </div>
  );
}
~~~

For a target inside the container, provide both container and target refs. Check that the element really overflows; without scrollable content, progress will not change.

## Keep scroll effects comfortable

Scroll-linked animation updates continuously as the scroll position changes. Prefer small changes in opacity, scale, and position. Large parallax movement can make reading difficult and may need a reduced-motion alternative.

A scroll-triggered animation changes state when an element crosses a threshold. A scroll-linked animation continuously maps progress to a value. Choose the one that matches the interaction rather than using continuous tracking by default.

## Practice questions

1. What values does useScroll provide?
2. What is the difference between scrollY and scrollYProgress?
3. What does the target option measure?
4. How does offset define the progress range?
5. Why use useTransform to map scroll progress?
6. How do you track a custom scrollable element?
7. What does useSpring add to a scroll-linked value?
8. How does a scroll-linked animation differ from a scroll-triggered animation?

## Main references

- [useScroll](https://motion.dev/docs/react-use-scroll)
- [useTransform](https://motion.dev/docs/react-use-transform)
- [useSpring](https://motion.dev/docs/react-use-spring)
- [Accessibility and reduced motion](https://motion.dev/docs/react-accessibility)