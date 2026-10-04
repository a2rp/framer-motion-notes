# 12. Sequences and imperative control

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Motion values and composition](./11-motion-values-and-composition.md) | [Notes index](../README.md) | [Next: SVG and path animation](./13-svg-and-path-animation.md) |

## Run an animation sequence with useAnimate

Most interface animations can be described with initial and animate props. useAnimate is useful when an event should run several steps in a particular order.

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

useAnimate returns a scope ref and an animate function. Attach the ref to a parent. Selectors passed to animate are scoped to that parent, so the same class elsewhere on the page is not accidentally changed. Awaiting the first animation makes the second begin after it completes.

The inline starting styles keep the items hidden until the event runs. In a real interface, ensure useful content remains available when animation code does not run. A checklist should not become inaccessible because a reveal effect failed.

## Describe a multi-step sequence

The animate function also accepts a sequence. Each entry describes a target, its animation values, and optional timing.

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

A sequence can run entries one after another or overlap them. The at option positions an entry relative to the previous sequence timing. Use overlap only when the relationship is clear; timing offsets are harder to maintain when many steps depend on one another.

## Control and stop an animation

The animate function returns animation controls. You can call stop on controls when a user action should cancel an active effect.

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

useAnimate handles the scope and lifecycle cleanup when the component unmounts. Stop an animation when the interaction requires cancellation before unmount, such as a dedicated stop button or switching to a different sequence.

## Choose declarative or imperative animation

Use declarative props when an element's visual state follows React state or a gesture. Use an imperative sequence for ordered steps, event-driven choreography, or a small group of elements that need direct control.

Keep application state in React. An animation sequence should communicate a state change, not become the only place where the application records whether an operation succeeded.

## Practice questions

1. What values does useAnimate return?
2. How does the scope ref limit selector queries?
3. Why can awaiting one animation help sequence the next?
4. What does stagger change?
5. What does the at option control in a sequence?
6. How can active animation controls be stopped?
7. When is an imperative sequence a better fit than declarative props?
8. Why should application state remain separate from animation progress?

## Main references

- [useAnimate](https://motion.dev/docs/react-use-animate)
- [Animation sequences](https://motion.dev/docs/sequence)
- [stagger](https://motion.dev/docs/stagger)
- [Motion values](https://motion.dev/docs/react-motion-value)