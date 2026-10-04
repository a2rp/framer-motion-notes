# 01. Motion for React setup and first animation

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Notes index](../README.md) | [Notes index](../README.md) | [Next: Motion components and animation values](./02-motion-components-and-animation-values.md) |

## Framer Motion and the current package

The animation library is now documented as Motion for React. The current package is named motion, and React components and hooks are imported from motion/react. Older projects may still use the framer-motion package and imports from framer-motion.

This repository uses the current package and import path in its examples. When updating an existing project, check its installed package version and the official upgrade guide before mixing examples from different releases.

## Install Motion

Motion for React supports React 18.2 and later. In an existing React project, add the package with the package manager:

~~~bash
npm install motion
~~~

The package manager updates the project manifest and lock file. Commit both files in an application repository so other machines install the same dependency tree.

Vite needs no additional configuration for a standard client app. In a Next.js App Router project, interactive animation components need a client boundary. Server components can use the documented motion/react-client entry when its constraints fit the component.

## Turn a normal element into a motion component

Import motion from motion/react and replace a regular HTML element with its motion equivalent. It keeps the element's normal HTML and React behavior while adding animation props.

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

The element starts with opacity zero and a small vertical offset. It moves to full opacity and its natural position. Motion handles the transition when the component mounts.

## Understand the three starting props

- initial describes the starting animation values.
- animate describes the target values.
- transition describes how the values move between those states.

Use a small distance and a short duration for a simple entrance. If an element should render immediately in its final state, use initial={false}.

Values such as opacity, x, y, scale, and rotate are common animation targets. x and y are pixel offsets, scale is a multiplier, and rotate is measured in degrees.

## Keep animation attached to meaningful state

An animation can respond to a React state change instead of only running on mount.

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

React owns the saved state. Motion interpolates the visual values between the target objects. The text and actual save operation should still work if animation is disabled.

## Make the first animation useful

A transition should help a user understand what changed. Use motion to show a new panel, confirm a state change, or guide attention. Avoid animating every element simply because the library makes it possible.

Start with one element, one state change, and one clear purpose. Check the interaction with a keyboard and touch input as well as a pointer.

## Practice questions

1. What package does the current Motion for React installation guide use?
2. Which module path exports React motion components?
3. What React version does the current installation guide require?
4. What does initial describe?
5. What does animate describe?
6. What does the transition prop control?
7. How does a state-driven animation relate to React state?
8. What should a useful entrance animation help a user understand?

## Main references

- [Motion for React installation](https://motion.dev/docs/react-installation)
- [Motion component](https://motion.dev/docs/react-motion-component)
- [React animation overview](https://motion.dev/docs/react-animation)
- [Upgrade guide](https://motion.dev/docs/react-upgrade-guide)
