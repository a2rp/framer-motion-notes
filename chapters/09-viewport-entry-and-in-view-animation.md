# 09. Viewport entry and in-view animation

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Layout and shared element animation](./08-layout-and-shared-element-animation.md) | [Notes index](../README.md) | [Next: Scroll-linked animation](./10-scroll-linked-animation.md) |

## Animate when an element enters the viewport

whileInView sets an animation target while the element is inside the viewport. The viewport option controls when the animation starts and whether it should repeat.

~~~jsx
import { motion } from "motion/react";

export function ReadingCard() {
  return (
    <motion.article
      initial={{ opacity: 0, y: 24 }}
      whileInView={{ opacity: 1, y: 0 }}
      viewport={{ once: true, amount: 0.25 }}
      transition={{ duration: 0.45, ease: "easeOut" }}
      style={{ maxWidth: 520, padding: 24, border: "1px solid #777" }}
    >
      <h2>Read the next section</h2>
      <p>The card appears when at least a quarter of it enters the viewport.</p>
    </motion.article>
  );
}
~~~

amount is the visible proportion required to count as entering. Values range from a small visible part to the whole element. once: true keeps the element in its entered state after the first time. Without it, the element can return to its initial state when it leaves and animate again when it re-enters.

## Stagger items as they enter

Use variants to let a parent coordinate children. The parent starts its entered state when it enters the viewport, then staggers the children.

~~~jsx
import { motion } from "motion/react";

const listVariants = {
  hidden: {},
  visible: {
    transition: { staggerChildren: 0.12 },
  },
};

const itemVariants = {
  hidden: { opacity: 0, y: 16 },
  visible: { opacity: 1, y: 0 },
};

const topics = ["Components", "Gestures", "Layout"];

export function TopicList() {
  return (
    <motion.ul
      variants={listVariants}
      initial="hidden"
      whileInView="visible"
      viewport={{ once: true, amount: 0.2 }}
    >
      {topics.map((topic) => (
        <motion.li key={topic} variants={itemVariants}>
          {topic}
        </motion.li>
      ))}
    </motion.ul>
  );
}
~~~

The parent variant controls the sequence while each child variant defines its own visual change. Keep enough of the list visible at the trigger point so the user understands what is appearing.

## Read viewport state with useInView

Use the hook when entering the viewport should change application content, not only an animation target.

~~~jsx
import { useRef } from "react";
import { useInView } from "motion/react";

export function SectionStatus() {
  const sectionRef = useRef(null);
  const isInView = useInView(sectionRef, { once: true, amount: 0.5 });

  return (
    <section ref={sectionRef} aria-live="polite">
      <h2>Database notes</h2>
      <p>{isInView ? "This section is in view." : "Scroll to this section."}</p>
    </section>
  );
}
~~~

useInView returns a boolean and observes the element attached to the ref. Use it for small state changes such as loading a section when it becomes relevant. For visual changes that do not require React state, whileInView can keep the work inside Motion.

## Choose a useful trigger point

A large element can enter the viewport before its main content is readable. Adjust amount to match the content. For a scrollable panel rather than the browser window, configure a root ref and attach it to the scrolling element.

Viewport entry should not hide content from users who do not scroll or whose browser does not run the animation. Keep initial content meaningful, and use reduced-motion preferences for animations that move or reveal large regions.

## Practice questions

1. What does whileInView control?
2. What does viewport.amount represent?
3. What changes when once is set to true?
4. How can variants stagger several items as their parent enters?
5. What does useInView return?
6. When is useInView a better fit than whileInView?
7. How can an element be observed inside a scrollable panel?
8. Why should the initial content remain useful if an animation does not run?

## Main references

- [whileInView and viewport options](https://motion.dev/docs/react-motion-component#viewport)
- [useInView](https://motion.dev/docs/react-use-in-view)
- [Variants](https://motion.dev/docs/react-variants)
- [Accessibility and reduced motion](https://motion.dev/docs/react-accessibility)