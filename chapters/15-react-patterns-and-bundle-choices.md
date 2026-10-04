# 15. React patterns and bundle choices

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Accessible motion and reduced motion](./14-accessible-motion-and-reduced-motion.md) | [Notes index](../README.md) | [Next: Performance, testing, and release checks](./16-performance-testing-and-release-checks.md) |

## Create custom Motion components outside render

motion.create turns a component that accepts a ref into a Motion component. Create it at module scope so React sees the same component type on every render.

~~~jsx
import { forwardRef } from "react";
import { motion } from "motion/react";

const Panel = forwardRef(function Panel(props, ref) {
  return <section ref={ref} {...props} />;
});

const MotionPanel = motion.create(Panel);

export function NotesPanel() {
  return (
    <MotionPanel
      initial={{ opacity: 0, y: 12 }}
      animate={{ opacity: 1, y: 0 }}
      style={{ padding: 20, border: "1px solid #888" }}
    >
      Content inside a reusable panel
    </MotionPanel>
  );
}
~~~

The wrapped component must forward the ref and pass style and other received props to the DOM element Motion measures or animates. Creating MotionPanel inside NotesPanel would produce a new component type on each render and can reset component state.

## Keep keys stable when animating lists

React keys identify which item is which across renders. Motion also uses those identities to connect layout and exit animations to the right element.

~~~jsx
import { AnimatePresence, motion } from "motion/react";

export function NoticeList({ notices }) {
  return (
    <ul>
      <AnimatePresence>
        {notices.map((notice) => (
          <motion.li
            key={notice.id}
            initial={{ opacity: 0, height: 0 }}
            animate={{ opacity: 1, height: "auto" }}
            exit={{ opacity: 0, height: 0 }}
          >
            {notice.message}
          </motion.li>
        ))}
      </AnimatePresence>
    </ul>
  );
}
~~~

Each notice needs a stable unique id. Array indexes can point to a different item after insertion or reordering, which can make React preserve the wrong state or animate the wrong row.

## Use Motion in server-rendered React projects

Motion's React Server Component entry point is motion/react-client. It supports rendering Motion components in server components where hooks and event handlers are not needed.

~~~jsx
import { motion } from "motion/react-client";

export function StaticIntro() {
  return (
    <motion.section initial={{ opacity: 0 }} animate={{ opacity: 1 }}>
      <h1>Motion in a server-rendered page</h1>
    </motion.section>
  );
}
~~~

Interactive components that use state, effects, gestures, or Motion hooks belong in a client component and use the motion/react entry point. Follow the framework's client boundary rules, and keep the client boundary close to the interaction that needs it.

## Load animation features on demand

A normal import of motion can include features your page does not use. LazyMotion with m lets an app load a chosen feature bundle.

~~~jsx
import { LazyMotion, domAnimation, m } from "motion/react";

export function SmallMotionBundle() {
  return (
    <LazyMotion features={domAnimation}>
      <m.div
        initial={{ opacity: 0 }}
        animate={{ opacity: 1 }}
        transition={{ duration: 0.25 }}
      >
        Animation features are provided by LazyMotion
      </m.div>
    </LazyMotion>
  );
}
~~~

domAnimation provides common animation and exit features. Projects that need drag or layout features can use the appropriate feature bundle, such as domMax, and should check the current package documentation. Do not switch to lazy loading without measuring the bundle and confirming that every required feature is available.

## Keep component state predictable

Keep animation state close to the component that owns the interaction. Use a boolean or selected item in React state to describe what should be visible, then use Motion props to animate the transition.

Avoid using animation callbacks as the only record that an important operation succeeded. The application should update its own state from the result of the operation, while animation reflects that state.

## Practice questions

1. Why should motion.create usually run outside a component render?
2. Which props must a custom wrapped component pass through for Motion to measure it?
3. How do stable keys help React and Motion?
4. Why can array indexes cause incorrect list behavior?
5. Which package entry point is intended for Motion components in React Server Components?
6. When should an interactive component use motion/react?
7. What are LazyMotion and m used for?
8. Why should the feature bundle match the animations actually used?

## Main references

- [Motion component and custom components](https://motion.dev/docs/react-motion-component)
- [React Server Components](https://motion.dev/docs/react-motion-component#server-components)
- [Reduce bundle size with LazyMotion](https://motion.dev/docs/react-lazy-motion)
- [AnimatePresence](https://motion.dev/docs/react-animate-presence)