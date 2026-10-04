# 08. Layout and shared element animation

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: AnimatePresence and component exit](./07-animatepresence-and-component-exit.md) | [Notes index](../README.md) | [Next: Viewport entry and in-view animation](./09-viewport-entry-and-in-view-animation.md) |

## Let Motion measure layout changes

React can change an element's size or position after state changes. Adding the layout prop asks Motion to measure the before and after layouts, then animate between them.

~~~jsx
import { useState } from "react";
import { motion } from "motion/react";

export function ExpandableCard() {
  const [expanded, setExpanded] = useState(false);

  return (
    <motion.section
      layout
      onClick={() => setExpanded((value) => !value)}
      style={{
        width: 280,
        padding: 20,
        border: "1px solid #555",
        borderRadius: 16,
        cursor: "pointer",
      }}
    >
      <motion.h2 layout="position">Project notes</motion.h2>
      {expanded && (
        <motion.p layout>
          This extra content changes the card height. Motion animates the
          measured layout change instead of requiring a guessed height.
        </motion.p>
      )}
    </motion.section>
  );
}
~~~

The layout prop works when a state change causes React to render a new layout. It does not make arbitrary CSS changes animate by itself. Keep the changing layout in React state or another clear source of truth.

layout="position" animates position while leaving size changes to normal layout. This can keep text from being scaled during a resize. Use layout when both position and size should move together.

## Animate a list when its order changes

Every item that should move needs layout. Use a stable key that identifies the item, such as its database id.

~~~jsx
import { useState } from "react";
import { motion } from "motion/react";

const startingTasks = [
  { id: "read", title: "Read the notes" },
  { id: "practice", title: "Run the example" },
  { id: "review", title: "Review the result" },
];

export function SortableTaskList() {
  const [tasks, setTasks] = useState(startingTasks);

  function moveFirstToEnd() {
    setTasks((current) => [...current.slice(1), current[0]]);
  }

  return (
    <section>
      <button type="button" onClick={moveFirstToEnd}>
        Move first task to the end
      </button>
      <ul>
        {tasks.map((task) => (
          <motion.li
            layout
            key={task.id}
            style={{ padding: 12, borderBottom: "1px solid #aaa" }}
          >
            {task.title}
          </motion.li>
        ))}
      </ul>
    </section>
  );
}
~~~

React still decides the order. Motion animates each keyed element from its old measured position to its new one. Avoid array indexes as keys when items can be inserted, removed, or reordered.

## Connect two elements with layoutId

A matching layoutId links elements across separate renders. Motion can animate the shared element from the old element's bounds to the new element's bounds.

~~~jsx
import { useState } from "react";
import { AnimatePresence, motion } from "motion/react";

export function ProjectDetails() {
  const [selected, setSelected] = useState(false);

  return (
    <div>
      <button type="button" onClick={() => setSelected((value) => !value)}>
        {selected ? "Close project" : "Open project"}
      </button>

      <AnimatePresence>
        {selected ? (
          <motion.article
            key="details"
            layoutId="project-card"
            initial={{ opacity: 0 }}
            animate={{ opacity: 1 }}
            exit={{ opacity: 0 }}
            style={{ padding: 24, border: "1px solid #888" }}
          >
            <h2>Study notes</h2>
            <p>Project description and recent changes.</p>
          </motion.article>
        ) : (
          <motion.button
            key="summary"
            type="button"
            layoutId="project-card"
            onClick={() => setSelected(true)}
            style={{ padding: 24, border: "1px solid #888" }}
          >
            Study notes
          </motion.button>
        )}
      </AnimatePresence>
    </div>
  );
}
~~~

The example includes a button that opens the detail view and a button inside the detail view that closes it. In a real card, keep the interactive element semantic and avoid nesting a button inside another button. A matching layoutId does not replace accessible controls.

Use unique layoutId values when several shared transitions can appear on one page. LayoutGroup can coordinate layout measurements for related components that do not share a direct React parent.

## Tune layout transitions

Layout animations use transforms to move between measured boxes. The visual result can differ slightly from normal CSS resizing, especially for borders, rounded corners, and shadows. Test the actual content and apply layout-aware styling only where the result needs adjustment.

You can pass a transition to the layout animation:

~~~jsx
<motion.div
  layout
  transition={{ layout: { duration: 0.28, ease: "easeOut" } }}
>
  Content that changes size or position
</motion.div>
~~~

Keep layout animation focused on meaningful changes. Animating a large page region after every small update can distract users and add unnecessary work.

## Practice questions

1. What does the layout prop measure and animate?
2. What needs to cause a render for a layout animation to run?
3. When can layout="position" be useful?
4. Why does each reordered list item need a stable key?
5. How does layoutId connect elements across renders?
6. Why should a shared layoutId be unique when multiple transitions may be visible?
7. What does LayoutGroup help coordinate?
8. Why should layout animations be tested with real text, borders, and shadows?

## Main references

- [Layout animation](https://motion.dev/docs/react-layout-animations)
- [AnimatePresence](https://motion.dev/docs/react-animate-presence)
- [Motion component](https://motion.dev/docs/react-motion-component)