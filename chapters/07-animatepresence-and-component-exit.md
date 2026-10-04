# 07. AnimatePresence and component exit

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Gestures, drag, and interaction states](./06-gestures-drag-and-interaction-states.md) | [Notes index](../README.md) | [Next: Layout and shared element animation](./08-layout-and-shared-element-animation.md) |

## Why a removed component needs presence handling

When React removes a component, it normally disappears from the DOM immediately. AnimatePresence detects when its direct child is removed and keeps it mounted until its exit animation completes.

~~~jsx
import { useState } from "react";
import { AnimatePresence, motion } from "motion/react";

export function HelpPanel() {
  const [open, setOpen] = useState(false);

  return (
    <section>
      <button type="button" onClick={() => setOpen((value) => !value)}>
        {open ? "Close help" : "Open help"}
      </button>

      <AnimatePresence>
        {open ? (
          <motion.aside
            key="help"
            initial={{ opacity: 0, y: 8 }}
            animate={{ opacity: 1, y: 0 }}
            exit={{ opacity: 0, y: 8 }}
          >
            Helpful information
          </motion.aside>
        ) : null}
      </AnimatePresence>
    </section>
  );
}
~~~

AnimatePresence must remain mounted while its children are conditionally added or removed. If the AnimatePresence component itself is removed with the child, it cannot coordinate the exit.

## Give direct children stable keys

AnimatePresence uses each direct child's key to tell which child left or changed. Use a stable record ID for list rows and a meaningful key for a changing page or panel.

~~~jsx
<AnimatePresence>
  {messages.map((message) => (
    <motion.li
      key={message.id}
      initial={{ opacity: 0, x: -8 }}
      animate={{ opacity: 1, x: 0 }}
      exit={{ opacity: 0, x: 8 }}
    >
      {message.text}
    </motion.li>
  ))}
</AnimatePresence>
~~~

Do not use an array index as a key when items can be inserted, deleted, or reordered. React and AnimatePresence need the identity to stay attached to the same item.

## Choose an exit mode

The default sync mode lets entering and exiting children animate at the same time. Use mode="wait" when one child should finish exiting before its replacement enters.

~~~jsx
<AnimatePresence mode="wait" initial={false}>
  <motion.article
    key={activePage}
    initial={{ opacity: 0, x: 16 }}
    animate={{ opacity: 1, x: 0 }}
    exit={{ opacity: 0, x: -16 }}
  >
    Page {activePage}
  </motion.article>
</AnimatePresence>
~~~

wait mode is best for a single changing child, such as a page panel or slideshow. For a list, use a mode that matches the desired behavior and test how siblings move.

initial={false} skips entrance animations for children present on the first render. This can avoid replaying a transition during server rendering or initial page display.

## Coordinate nested presence boundaries

A nested AnimatePresence creates a new boundary for the exit animations it controls. If an inner component should also play its exit when an outer child leaves, configure propagation according to the current API and test the nested behavior.

Use the simplest boundary structure that matches component ownership. Too many nested presence managers make it harder to understand which component is waiting for which exit.

## Practice questions

1. What does AnimatePresence detect?
2. Why must AnimatePresence remain mounted around conditional children?
3. What does a child key tell AnimatePresence?
4. Why can array indexes be unsafe keys for changing lists?
5. What is the default behavior when entering and exiting children overlap?
6. When is mode="wait" useful?
7. What does initial={false} change?
8. Why should nested presence boundaries be used deliberately?

## Main references

- [AnimatePresence](https://motion.dev/docs/react-animate-presence)
- [React animation overview](https://motion.dev/docs/react-animation)
- [Layout animation and AnimatePresence](https://motion.dev/docs/react-layout-animations)
