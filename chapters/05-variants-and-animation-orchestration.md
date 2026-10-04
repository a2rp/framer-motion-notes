# 05. Variants and animation orchestration

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Transitions, easing, and springs](./04-transitions-easing-and-springs.md) | [Notes index](../README.md) | [Next: Gestures, drag, and interaction states](./06-gestures-drag-and-interaction-states.md) |

## Name reusable animation states

Variants are named animation targets. A component can select a label such as hidden or visible instead of repeating the same target object in several props.

~~~jsx
import { motion } from "motion/react";

const panelVariants = {
  hidden: { opacity: 0, y: 12 },
  visible: { opacity: 1, y: 0 },
};

export function SearchPanel() {
  return (
    <motion.section
      variants={panelVariants}
      initial="hidden"
      animate="visible"
    >
      Search results
    </motion.section>
  );
}
~~~

Variants are useful when multiple components share the same state names. Keep the names and values close to the component or feature that owns them.

## Let variants flow to children

When a parent motion component changes to a variant label, child motion components with matching variants can follow it. This keeps a list or menu coordinated.

~~~jsx
import { motion } from "motion/react";

const listVariants = {
  hidden: { opacity: 0 },
  visible: {
    opacity: 1,
    transition: { delayChildren: 0.08 },
  },
};

const itemVariants = {
  hidden: { opacity: 0, y: 8 },
  visible: { opacity: 1, y: 0 },
};

export function ResultList({ results }) {
  return (
    <motion.ul
      variants={listVariants}
      initial="hidden"
      animate="visible"
    >
      {results.map((result) => (
        <motion.li key={result.id} variants={itemVariants}>
          {result.title}
        </motion.li>
      ))}
    </motion.ul>
  );
}
~~~

Each rendered React item still needs a stable key. Variant propagation controls animation state, while React keys identify the individual records.

## Stagger child animations

Import stagger from motion/react and use it in delayChildren to offset each child start.

~~~jsx
import { motion, stagger } from "motion/react";

const listVariants = {
  hidden: { opacity: 0 },
  visible: {
    opacity: 1,
    transition: {
      delayChildren: stagger(0.07),
    },
  },
};

const itemVariants = {
  hidden: { opacity: 0, y: 10 },
  visible: { opacity: 1, y: 0 },
};
~~~

Stagger is useful for short menus or a small set of results. A long list should not make users wait for every row to animate. Choose a modest delay or animate only the first visible group.

The from option can stagger from the last item, center, or a specific index.

~~~js
const delayFromCenter = stagger(0.06, { from: "center" });
~~~

## Order parent and child transitions

The when setting controls whether a parent transition runs before or after child transitions.

~~~js
const panelVariants = {
  hidden: {
    opacity: 0,
    transition: { when: "afterChildren" },
  },
  visible: {
    opacity: 1,
    transition: {
      when: "beforeChildren",
      delayChildren: stagger(0.05),
    },
  },
};
~~~

Use orchestration only when the sequence helps explain the interface change. If the parent and children can move at the same time without confusion, the default is simpler.

## Create a variant from item data

A variant can be a function that reads the component's custom value. This can provide an index or direction without creating a separate variant object for each item.

~~~jsx
import { motion } from "motion/react";

const rowVariants = {
  hidden: { opacity: 0 },
  visible: (index) => ({
    opacity: 1,
    x: 0,
    transition: { delay: index * 0.04 },
  }),
};

export function NumberedRows({ rows }) {
  return rows.map((row, index) => (
    <motion.div
      key={row.id}
      custom={index}
      variants={rowVariants}
      initial="hidden"
      animate="visible"
      style={{ x: -8 }}
    >
      {row.label}
    </motion.div>
  ));
}
~~~

Keep dynamic values predictable. For complex state, pass a small clear value such as direction or index rather than an entire record.

## Practice questions

1. What problem do named variants solve?
2. How can a parent variant coordinate child motion components?
3. Why does each mapped React child still need a stable key?
4. What does stagger change?
5. What does the from option control?
6. How does when order parent and child animations?
7. How does a dynamic variant receive an item-specific value?
8. When can staggering a long list harm the interface?

## Main references

- [Variants and orchestration](https://motion.dev/docs/react-animation#variants)
- [Stagger](https://motion.dev/docs/stagger)
- [React transitions](https://motion.dev/docs/react-transitions)
- [Motion for React examples](https://motion.dev/examples/react-variants)
