# 98. All code samples

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Performance, testing, and release checks](./16-performance-testing-and-release-checks.md) | [Notes index](../README.md) | [Next: Complete questions and answers](./99-complete-q-and-a.md) |

## Source chapter: [01. Motion for React setup and first animation](./01-motion-for-react-setup-and-first-animation.md)

### Sample 1

~~~bash
npm install motion
~~~

### Sample 2

~~~jsx
import { motion } from "motion/react";

export function NoticeCard() {
  return (
    <motion.section
      initial={{ opacity: 0, y: 16 }}
      animate={{ opacity: 1, y: 0 }}
      transition={{ duration: 0.35, ease: "easeOut" }}
    >
      <h2>Workspace ready</h2>
      <p>Your saved items are available.</p>
    </motion.section>
  );
}
~~~

### Sample 3

~~~jsx
import { useState } from "react";
import { motion } from "motion/react";

export function SaveButton() {
  const [saved, setSaved] = useState(false);

  return (
    <motion.button
      type="button"
      onClick={() => setSaved((value) => !value)}
      animate={{
        scale: saved ? 1.04 : 1,
        backgroundColor: saved ? "#176b4d" : "#222222",
      }}
      transition={{ duration: 0.18 }}
    >
      {saved ? "Saved" : "Save item"}
    </motion.button>
  );
}
~~~

## Source chapter: [02. Motion components and animation values](./02-motion-components-and-animation-values.md)

### Sample 1

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

### Sample 2

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

### Sample 3

~~~jsx
<motion.div
  animate={{ x: 24, rotate: 2, scale: 1.02 }}
  transition={{ duration: 0.2 }}
/>
~~~

### Sample 4

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

## Source chapter: [03. Initial, animate, exit, and keyframes](./03-initial-animate-exit-and-keyframes.md)

### Sample 1

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

### Sample 2

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

### Sample 3

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

### Sample 4

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

## Source chapter: [04. Transitions, easing, and springs](./04-transitions-easing-and-springs.md)

### Sample 1

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

### Sample 2

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

### Sample 3

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

### Sample 4

~~~jsx
<motion.aside
  animate={{ x: 0, opacity: 1 }}
  transition={{
    default: { type: "spring", stiffness: 260, damping: 28 },
    opacity: { type: "tween", duration: 0.2 },
  }}
/>
~~~

### Sample 5

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

### Sample 6

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

## Source chapter: [05. Variants and animation orchestration](./05-variants-and-animation-orchestration.md)

### Sample 1

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

### Sample 2

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

### Sample 3

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

### Sample 4

~~~js
const delayFromCenter = stagger(0.06, { from: "center" });
~~~

### Sample 5

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

### Sample 6

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

## Source chapter: [06. Gestures, drag, and interaction states](./06-gestures-drag-and-interaction-states.md)

### Sample 1

~~~jsx
import { motion } from "motion/react";

export function ActionButton() {
  return (
    <motion.button
      type="button"
      whileHover={{ y: -2 }}
      whileTap={{ scale: 0.97 }}
      whileFocus={{ outline: "2px solid #e85b24" }}
      transition={{ duration: 0.15 }}
    >
      Create note
    </motion.button>
  );
}
~~~

### Sample 2

~~~jsx
import { useRef } from "react";
import { motion } from "motion/react";

export function DragCard() {
  const boundaryRef = useRef(null);

  return (
    <div
      ref={boundaryRef}
      style={{
        width: 320,
        height: 180,
        border: "1px solid #aaa",
        position: "relative",
      }}
    >
      <motion.div
        drag
        dragConstraints={boundaryRef}
        dragElastic={0.08}
        dragMomentum={false}
        whileDrag={{ scale: 1.04 }}
        style={{
          width: 110,
          padding: 12,
          background: "#f0e6df",
          cursor: "grab",
        }}
      >
        Move this card
      </motion.div>
    </div>
  );
}
~~~

### Sample 3

~~~jsx
import { motion } from "motion/react";

export function PanSurface() {
  function handlePan(event, info) {
    console.log(info.offset.x, info.offset.y);
  }

  return (
    <motion.div
      onPan={handlePan}
      style={{
        touchAction: "none",
        padding: 24,
        background: "#ececec",
      }}
    >
      Drag a pointer across this area
    </motion.div>
  );
}
~~~

## Source chapter: [07. AnimatePresence and component exit](./07-animatepresence-and-component-exit.md)

### Sample 1

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

### Sample 2

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

### Sample 3

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

## Source chapter: [08. Layout and shared element animation](./08-layout-and-shared-element-animation.md)

### Sample 1

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

### Sample 2

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

### Sample 3

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

### Sample 4

~~~jsx
<motion.div
  layout
  transition={{ layout: { duration: 0.28, ease: "easeOut" } }}
>
  Content that changes size or position
</motion.div>
~~~

## Source chapter: [09. Viewport entry and in-view animation](./09-viewport-entry-and-in-view-animation.md)

### Sample 1

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

### Sample 2

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

### Sample 3

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

## Source chapter: [10. Scroll-linked animation](./10-scroll-linked-animation.md)

### Sample 1

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

### Sample 2

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

### Sample 3

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

## Source chapter: [11. Motion values and composition](./11-motion-values-and-composition.md)

### Sample 1

~~~jsx
import { useMotionValue, motion } from "motion/react";

export function PointerFollower() {
  const x = useMotionValue(0);
  const y = useMotionValue(0);

  function movePointer(event) {
    x.set(event.clientX);
    y.set(event.clientY);
  }

  return (
    <div
      onPointerMove={movePointer}
      style={{ height: 240, border: "1px solid #888", position: "relative" }}
    >
      <motion.div
        style={{
          x,
          y,
          width: 24,
          height: 24,
          borderRadius: "50%",
          background: "#e85b24",
          position: "absolute",
          top: 0,
          left: 0,
          pointerEvents: "none",
        }}
      />
      Move your pointer inside this area
    </div>
  );
}
~~~

### Sample 2

~~~jsx
import { motion, useMotionValue, useTransform } from "motion/react";

export function TiltCard() {
  const pointerX = useMotionValue(0);
  const rotate = useTransform(pointerX, [-0.5, 0.5], [-7, 7]);

  function updatePointer(event) {
    const bounds = event.currentTarget.getBoundingClientRect();
    const normalizedX = (event.clientX - bounds.left) / bounds.width - 0.5;
    pointerX.set(normalizedX);
  }

  return (
    <motion.div
      onPointerMove={updatePointer}
      onPointerLeave={() => pointerX.set(0)}
      style={{ rotate, padding: 24, border: "1px solid #888" }}
    >
      Move across this card
    </motion.div>
  );
}
~~~

### Sample 3

~~~jsx
import { motion, useMotionValue, useSpring } from "motion/react";

export function SmoothFollower() {
  const sourceX = useMotionValue(0);
  const x = useSpring(sourceX, { stiffness: 220, damping: 24 });

  return (
    <motion.div
      onPointerMove={(event) => sourceX.set(event.clientX)}
      style={{ x, padding: 16, border: "1px solid #888" }}
    >
      Move the pointer to see the spring follow
    </motion.div>
  );
}
~~~

### Sample 4

~~~jsx
import { useMotionValue, useMotionValueEvent } from "motion/react";

export function ValueObserver() {
  const x = useMotionValue(0);

  useMotionValueEvent(x, "change", (latest) => {
    if (latest > 200) {
      console.log("The value passed 200 pixels");
    }
  });

  return (
    <button type="button" onClick={() => x.set(x.get() + 50)}>
      Move value to {x.get()} pixels
    </button>
  );
}
~~~

## Source chapter: [12. Sequences and imperative control](./12-sequences-and-imperative-control.md)

### Sample 1

~~~jsx
import { useAnimate, stagger } from "motion/react";

export function RevealChecklist() {
  const [scope, animate] = useAnimate();

  async function revealItems() {
    await animate(
      "li",
      { opacity: 1, x: 0 },
      { duration: 0.25, delay: stagger(0.12) }
    );
    await animate(
      ".complete",
      { opacity: 1, y: 0 },
      { duration: 0.2 }
    );
  }

  return (
    <section ref={scope}>
      <button type="button" onClick={revealItems}>
        Reveal checklist
      </button>
      <ul>
        <li style={{ opacity: 0, transform: "translateX(12px)" }}>
          Read the section
        </li>
        <li style={{ opacity: 0, transform: "translateX(12px)" }}>
          Try the example
        </li>
        <li style={{ opacity: 0, transform: "translateX(12px)" }}>
          Review the result
        </li>
      </ul>
      <p
        className="complete"
        style={{ opacity: 0, transform: "translateY(8px)" }}
      >
        All steps are visible.
      </p>
    </section>
  );
}
~~~

### Sample 2

~~~jsx
import { useAnimate, stagger } from "motion/react";

export function SequenceExample() {
  const [scope, animate] = useAnimate();

  async function playSequence() {
    await animate([
      ["h2", { opacity: 1, y: 0 }, { duration: 0.25 }],
      ["li", { opacity: 1, x: 0 }, { delay: stagger(0.1), at: "<" }],
      [".finish", { opacity: 1 }, { at: ">-0.1" }],
    ]);
  }

  return (
    <section ref={scope}>
      <button type="button" onClick={playSequence}>
        Play sequence
      </button>
      <h2 style={{ opacity: 0, transform: "translateY(8px)" }}>Steps</h2>
      <ul>
        <li style={{ opacity: 0, transform: "translateX(10px)" }}>First</li>
        <li style={{ opacity: 0, transform: "translateX(10px)" }}>Second</li>
      </ul>
      <p className="finish" style={{ opacity: 0 }}>Complete</p>
    </section>
  );
}
~~~

### Sample 3

~~~jsx
import { useRef } from "react";
import { useAnimate } from "motion/react";

export function CancellableAnimation() {
  const [scope, animate] = useAnimate();
  const controlsRef = useRef(null);

  async function start() {
    controlsRef.current = animate(
      ".panel",
      { x: [0, 120, 0] },
      { duration: 1.2 }
    );
  }

  function stop() {
    controlsRef.current?.stop();
  }

  return (
    <section ref={scope}>
      <button type="button" onClick={start}>Start</button>
      <button type="button" onClick={stop}>Stop</button>
      <div className="panel" style={{ width: 80, height: 40, background: "#e85b24" }} />
    </section>
  );
}
~~~

## Source chapter: [13. SVG and path animation](./13-svg-and-path-animation.md)

### Sample 1

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

### Sample 2

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

### Sample 3

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

## Source chapter: [14. Accessible motion and reduced motion](./14-accessible-motion-and-reduced-motion.md)

### Sample 1

~~~jsx
import { MotionConfig, motion } from "motion/react";

export function AppMotion() {
  return (
    <MotionConfig reducedMotion="user">
      <motion.main
        initial={{ opacity: 0, y: 16 }}
        animate={{ opacity: 1, y: 0 }}
      >
        <h1>Study notes</h1>
        <p>The content remains available while the entrance effect runs.</p>
      </motion.main>
    </MotionConfig>
  );
}
~~~

### Sample 2

~~~jsx
import { motion, useReducedMotion } from "motion/react";

export function MotionAwareNotice() {
  const shouldReduceMotion = useReducedMotion();

  return (
    <motion.aside
      initial={shouldReduceMotion ? { opacity: 0 } : { opacity: 0, y: 24 }}
      animate={{ opacity: 1, y: 0 }}
      transition={{
        duration: shouldReduceMotion ? 0.15 : 0.4,
      }}
      style={{ padding: 20, border: "1px solid #888" }}
    >
      <h2>Saved</h2>
      <p>Your notes are available in the list.</p>
    </motion.aside>
  );
}
~~~

### Sample 3

~~~jsx
import { motion } from "motion/react";

export function SaveButton({ onSave }) {
  return (
    <motion.button
      type="button"
      onClick={onSave}
      whileHover={{ y: -1 }}
      whileTap={{ scale: 0.98 }}
      whileFocus={{ outline: "2px solid #e85b24", outlineOffset: 3 }}
    >
      Save notes
    </motion.button>
  );
}
~~~

## Source chapter: [15. React patterns and bundle choices](./15-react-patterns-and-bundle-choices.md)

### Sample 1

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

### Sample 2

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

### Sample 3

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

### Sample 4

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

## Source chapter: [16. Performance, testing, and release checks](./16-performance-testing-and-release-checks.md)

This chapter has no fenced code samples.

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Performance, testing, and release checks](./16-performance-testing-and-release-checks.md) | [Notes index](../README.md) | [Next: Complete questions and answers](./99-complete-q-and-a.md) |
