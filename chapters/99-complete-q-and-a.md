# 99. Complete questions and answers

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: All code samples](./98-all-code-samples.md) | [Notes index](../README.md) | End of notes |

## 01. [01. Motion for React setup and first animation](./01-motion-for-react-setup-and-first-animation.md)

### Question 1: What package does the current Motion for React installation guide use?

**Answer:** The current guide installs the motion package with npm install motion.

### Question 2: Which module path exports React motion components?

**Answer:** React motion components are imported from motion/react.

### Question 3: What React version does the current installation guide require?

**Answer:** The current installation guide requires React 18.2 or later.

### Question 4: What does initial describe?

**Answer:** initial describes the visual values used before the animation reaches its target.

### Question 5: What does animate describe?

**Answer:** animate describes the target values Motion should animate toward.

### Question 6: What does the transition prop control?

**Answer:** transition configures how values change, including duration, delay, easing, and repeat behavior.

### Question 7: How does a state-driven animation relate to React state?

**Answer:** React state selects the interface state. Motion animates the component toward the target for that state.

### Question 8: What should a useful entrance animation help a user understand?

**Answer:** It should clarify a meaningful change, such as where a panel came from or which action just completed.

## 02. [02. Motion components and animation values](./02-motion-components-and-animation-values.md)

### Question 1: Which motion component should be used for a semantic button?

**Answer:** Use motion.button so the control keeps native button semantics and can receive Motion props.

### Question 2: Can a motion component render an SVG element?

**Answer:** Yes. Motion provides SVG components such as motion.svg, motion.path, and motion.circle.

### Question 3: Which usual React styling props can a motion component receive?

**Answer:** It can receive props such as className, style, and ordinary DOM attributes, along with Motion props.

### Question 4: What do x, y, scale, and rotate represent?

**Answer:** They represent horizontal movement, vertical movement, scaling, and rotation.

### Question 5: Why should semantic HTML be preserved in animated interfaces?

**Answer:** Semantic HTML provides the expected roles, keyboard behavior, and meaning to assistive technology.

### Question 6: What must a custom component provide so Motion can animate it?

**Answer:** It must forward the ref and pass relevant props, especially style, to the DOM element Motion needs to measure or animate.

### Question 7: Where should motion.create be called?

**Answer:** Call motion.create outside component render so the wrapped component type stays stable between renders.

### Question 8: Which values are often suitable for frequent visual movement?

**Answer:** Transforms such as x, y, scale, and rotate, plus opacity, are often suitable for frequent visual movement.

## 03. [03. Initial, animate, exit, and keyframes](./03-initial-animate-exit-and-keyframes.md)

### Question 1: What does initial describe?

**Answer:** initial describes the starting visual target before the first animation.

### Question 2: What does animate describe?

**Answer:** animate describes the current target values.

### Question 3: What happens when an animate target changes?

**Answer:** Motion transitions from the current values to the new animate target.

### Question 4: How does initial={false} change the first render?

**Answer:** initial={false} skips the initial state animation for elements present on the first render.

### Question 5: How are keyframes represented in an animate target?

**Answer:** A keyframe value is an array of values, such as opacity: [0, 1, 0.5].

### Question 6: What does times control?

**Answer:** times maps keyframes to positions in the animation timeline, using normalized values from zero to one.

### Question 7: Why should UI state remain separate from its visual animation?

**Answer:** React state records what the interface means; animation only presents the visual change.

### Question 8: What does AnimatePresence do for a removed component?

**Answer:** AnimatePresence keeps a removed child mounted long enough to run its exit animation.

## 04. [04. Transitions, easing, and springs](./04-transitions-easing-and-springs.md)

### Question 1: What does a transition configure?

**Answer:** A transition configures the timing and behavior used to reach an animation target.

### Question 2: When is a tween useful?

**Answer:** A tween is useful when a change should follow a predictable fixed duration and easing curve.

### Question 3: What does easeOut do?

**Answer:** easeOut starts quickly and slows as it approaches the target.

### Question 4: What does spring stiffness control?

**Answer:** Stiffness controls how strongly a spring pulls toward its target. Higher stiffness generally responds faster.

### Question 5: How does damping affect a spring?

**Answer:** Damping reduces spring oscillation. Too little damping can cause more visible bouncing.

### Question 6: When can a duration-based spring be useful?

**Answer:** A duration-based spring is useful when the movement should keep spring-like behavior but fit a predictable time.

### Question 7: How can position and opacity use different transitions?

**Answer:** Put a transition object on each property, such as separate transition settings for x and opacity.

### Question 8: What should be considered before using an infinite repeat?

**Answer:** Consider whether repetition has a clear purpose, whether it can distract, and whether users can pause or avoid it.

## 05. [05. Variants and animation orchestration](./05-variants-and-animation-orchestration.md)

### Question 1: What problem do named variants solve?

**Answer:** Named variants give reusable labels to visual states and keep related targets organized.

### Question 2: How can a parent variant coordinate child motion components?

**Answer:** A parent variant can set a label that matching child variants inherit, coordinating their state changes.

### Question 3: Why does each mapped React child still need a stable key?

**Answer:** Stable keys let React preserve each item identity and let Motion animate the correct child.

### Question 4: What does stagger change?

**Answer:** Stagger delays the start of children relative to one another.

### Question 5: What does the from option control?

**Answer:** The from option chooses where the stagger begins, for example at the first, last, or center item.

### Question 6: How does when order parent and child animations?

**Answer:** when controls whether the parent animates before or after its children.

### Question 7: How does a dynamic variant receive an item-specific value?

**Answer:** Pass item-specific data through custom and read it in a dynamic variant function.

### Question 8: When can staggering a long list harm the interface?

**Answer:** A long stagger can make a list feel slow, delay access to information, or distract from reading.

## 06. [06. Gestures, drag, and interaction states](./06-gestures-drag-and-interaction-states.md)

### Question 1: Which while props provide hover, tap, focus, and drag feedback?

**Answer:** whileHover, whileTap, whileFocus, and whileDrag describe temporary targets for those active interactions.

### Question 2: Why should a motion button still have a real event handler?

**Answer:** The animation only changes appearance. An event handler such as onClick still performs the button action.

### Question 3: How can drag be limited to one axis?

**Answer:** Set drag to x or y to constrain movement to that axis.

### Question 4: What does dragConstraints accept?

**Answer:** dragConstraints can receive a ref to a boundary element or numeric limits for movement.

### Question 5: What is the difference between dragMomentum and dragElastic?

**Answer:** dragMomentum controls inertia after release; dragElastic controls how far movement can stretch beyond constraints.

### Question 6: Which data does a pan callback receive?

**Answer:** A pan callback receives the pointer event and an info object with values such as point, delta, offset, and velocity.

### Question 7: Why can touch-action affect a pan gesture?

**Answer:** touch-action tells the browser which touch gestures it may handle, which can otherwise compete with pointer tracking.

### Question 8: Why should dragging not be the only way to complete an important task?

**Answer:** Dragging can be difficult or impossible for some users, so provide a keyboard or button-based way to perform the task.

## 07. [07. AnimatePresence and component exit](./07-animatepresence-and-component-exit.md)

### Question 1: What does AnimatePresence detect?

**Answer:** AnimatePresence detects when its direct React children are removed or replaced.

### Question 2: Why must AnimatePresence remain mounted around conditional children?

**Answer:** It must stay mounted around the conditional children so it can observe their removal and run exit animations.

### Question 3: What does a child key tell AnimatePresence?

**Answer:** A key identifies the child instance, allowing Motion to distinguish an exiting element from a new one.

### Question 4: Why can array indexes be unsafe keys for changing lists?

**Answer:** After insertions or reordering, an index can identify a different item, so the wrong component state or exit animation may be retained.

### Question 5: What is the default behavior when entering and exiting children overlap?

**Answer:** The default sync behavior allows entering and exiting children to animate at the same time.

### Question 6: When is mode="wait" useful?

**Answer:** mode="wait" is useful when one child should finish exiting before the next child enters, such as a single page panel.

### Question 7: What does initial={false} change?

**Answer:** initial={false} skips the entrance animation for children rendered on the initial mount.

### Question 8: Why should nested presence boundaries be used deliberately?

**Answer:** Nested boundaries affect which manager observes an exit and whether nested children are included, so ownership should be clear.

## 08. [08. Layout and shared element animation](./08-layout-and-shared-element-animation.md)

### Question 1: What does the layout prop measure and animate?

**Answer:** layout measures an element before and after a React layout change, then animates between the measured boxes.

### Question 2: What needs to cause a render for a layout animation to run?

**Answer:** A state or data change must cause React to render the new layout for Motion to compare.

### Question 3: When can layout="position" be useful?

**Answer:** layout="position" is useful when position should animate but the element size should change without being scaled.

### Question 4: Why does each reordered list item need a stable key?

**Answer:** Stable keys keep each item identity connected to its previous and new position.

### Question 5: How does layoutId connect elements across renders?

**Answer:** Elements with the same layoutId can animate between their measured bounds across renders.

### Question 6: Why should a shared layoutId be unique when multiple transitions may be visible?

**Answer:** Unique identifiers prevent unrelated visible elements from being treated as one shared transition.

### Question 7: What does LayoutGroup help coordinate?

**Answer:** LayoutGroup coordinates layout measurements among related components that may not share a direct React parent.

### Question 8: Why should layout animations be tested with real text, borders, and shadows?

**Answer:** Real content can change wrapping and measured sizes, while borders and shadows can reveal visual artifacts from transform-based resizing.

## 09. [09. Viewport entry and in-view animation](./09-viewport-entry-and-in-view-animation.md)

### Question 1: What does whileInView control?

**Answer:** whileInView sets an animation target while its element meets the viewport visibility condition.

### Question 2: What does viewport.amount represent?

**Answer:** viewport.amount is the proportion of the element that must be visible to count as in view.

### Question 3: What changes when once is set to true?

**Answer:** once: true means the element stays in its entered state after its first viewport entry.

### Question 4: How can variants stagger several items as their parent enters?

**Answer:** Give the parent and children variants, then use staggerChildren in the parent transition when it enters.

### Question 5: What does useInView return?

**Answer:** useInView returns a boolean indicating whether the referenced element is in view.

### Question 6: When is useInView a better fit than whileInView?

**Answer:** useInView is a better fit when viewport entry must affect application logic or other rendered content, not only visual animation.

### Question 7: How can an element be observed inside a scrollable panel?

**Answer:** Pass the scrolling element ref as the root option and attach it to the scroll container.

### Question 8: Why should the initial content remain useful if an animation does not run?

**Answer:** Users may not scroll or animations may be unavailable, so the initial content should still communicate useful information.

## 10. [10. Scroll-linked animation](./10-scroll-linked-animation.md)

### Question 1: What values does useScroll provide?

**Answer:** useScroll provides scrollX, scrollY, scrollXProgress, and scrollYProgress Motion values.

### Question 2: What is the difference between scrollY and scrollYProgress?

**Answer:** scrollY is the vertical pixel position; scrollYProgress is normalized progress from zero to one.

### Question 3: What does the target option measure?

**Answer:** target measures progress through a particular element as it crosses the configured offsets.

### Question 4: How does offset define the progress range?

**Answer:** offset chooses the target and container intersection points that mark the beginning and end of progress.

### Question 5: Why use useTransform to map scroll progress?

**Answer:** useTransform maps scroll progress to another range, such as opacity, scale, or position, without setting React state every frame.

### Question 6: How do you track a custom scrollable element?

**Answer:** Attach a ref to the scrollable element and pass it as the container option.

### Question 7: What does useSpring add to a scroll-linked value?

**Answer:** useSpring smooths changes by making the output spring toward the source value, which adds some lag.

### Question 8: How does a scroll-linked animation differ from a scroll-triggered animation?

**Answer:** A linked animation continuously maps scroll progress to visual values; a triggered animation changes state when a threshold is crossed.

## 11. [11. Motion values and composition](./11-motion-values-and-composition.md)

### Question 1: What does useMotionValue create?

**Answer:** useMotionValue creates a Motion-managed value that can be updated and passed into Motion styles.

### Question 2: Why can Motion values update visuals without a React render for every frame?

**Answer:** Motion updates subscribed visual properties directly, so every frame does not need to schedule a React render.

### Question 3: How does useTransform derive an output from an input?

**Answer:** useTransform maps an input Motion value or range to a derived output value or range.

### Question 4: When can useSpring improve a Motion value?

**Answer:** useSpring is useful when a direct value change should be followed with a smoother spring response.

### Question 5: What does useMotionValueEvent subscribe to?

**Answer:** useMotionValueEvent subscribes to events such as change on a Motion value and cleans up with the component lifecycle.

### Question 6: Why might a live text readout still require React state?

**Answer:** Text is rendered by React, so a changing textual value needs a render or a dedicated Motion-rendered output.

### Question 7: Which values belong in Motion values and which belong in React state?

**Answer:** Use Motion values for fast-changing visual values; use React state for content, decisions, and data that changes the component tree.

### Question 8: What should be considered before building a pointer-following effect?

**Answer:** Consider touch and keyboard behavior, coordinate bounds, reduced motion, pointer leaving, and whether the effect helps the task.

## 12. [12. Sequences and imperative control](./12-sequences-and-imperative-control.md)

### Question 1: What values does useAnimate return?

**Answer:** useAnimate returns a scope ref and an animate function.

### Question 2: How does the scope ref limit selector queries?

**Answer:** Attach the scope ref to a parent; selectors passed to animate are queried only inside that element.

### Question 3: Why can awaiting one animation help sequence the next?

**Answer:** Awaiting a returned animation promise lets the next step start after the current animation finishes.

### Question 4: What does stagger change?

**Answer:** stagger adds a delay between the start times of selected elements.

### Question 5: What does the at option control in a sequence?

**Answer:** The at option positions a sequence entry relative to the previous animation timeline.

### Question 6: How can active animation controls be stopped?

**Answer:** Keep the returned animation controls and call stop on them when the interaction should cancel the animation.

### Question 7: When is an imperative sequence a better fit than declarative props?

**Answer:** An imperative sequence fits ordered, event-driven choreography involving one or more elements.

### Question 8: Why should application state remain separate from animation progress?

**Answer:** React state records whether an operation or interface change happened; animation progress is only its visual presentation.

## 13. [13. SVG and path animation](./13-svg-and-path-animation.md)

### Question 1: Which SVG elements have Motion component versions?

**Answer:** Motion includes SVG components such as motion.svg, motion.path, motion.circle, and motion.rect.

### Question 2: What does the SVG viewBox describe?

**Answer:** viewBox defines the SVG coordinate system and how it maps into the rendered viewport.

### Question 3: What produces a path drawing effect?

**Answer:** Animating pathLength from zero to one draws a visible stroked path.

### Question 4: Why does a path drawing example need a stroke?

**Answer:** The stroke renders the outline that is progressively revealed; fill alone does not create the same line drawing effect.

### Question 5: How can variants sequence multiple SVG paths?

**Answer:** Give the parent and child paths variants, then stagger the child transitions from the parent.

### Question 6: How should a decorative SVG be exposed to assistive technology?

**Answer:** Mark an SVG that adds no information with aria-hidden="true".

### Question 7: Why can path morphing fail between unrelated d values?

**Answer:** Path morphing interpolates corresponding commands, so unrelated path structures may not map to each other correctly.

### Question 8: What should be considered before repeating an SVG animation?

**Answer:** Check whether repetition is useful, distracting, accessible, and stoppable when it could interfere with reading.

## 14. [14. Accessible motion and reduced motion](./14-accessible-motion-and-reduced-motion.md)

### Question 1: What does reducedMotion="user" read?

**Answer:** reducedMotion="user" follows the reduced-motion preference reported by the user's operating system or browser.

### Question 2: Which animation types does Motion disable by default under reduced motion?

**Answer:** Motion disables transform and layout animations by default while reduced motion is active; opacity and color can remain.

### Question 3: Why should every interaction still be reviewed after setting MotionConfig?

**Answer:** Each interaction can have different movement, duration, and repetition, so the global setting may not remove every uncomfortable effect.

### Question 4: What does useReducedMotion return?

**Answer:** useReducedMotion returns whether the user has requested reduced motion.

### Question 5: When might removing an animation be better than replacing it with a fade?

**Answer:** Removing motion is better when even a fade is distracting or the effect provides no necessary information.

### Question 6: Why do semantic buttons remain necessary for animated controls?

**Answer:** Semantic buttons supply accessible role and keyboard behavior that an animation cannot provide.

### Question 7: What should replace a removed browser focus indicator?

**Answer:** Provide a visible replacement focus style so keyboard users can still see which control is active.

### Question 8: Which movement patterns can make content uncomfortable or difficult to follow?

**Answer:** Rapid flashing, large parallax movement, long travel, and repeated movement can cause discomfort or interrupt reading.

## 15. [15. React patterns and bundle choices](./15-react-patterns-and-bundle-choices.md)

### Question 1: Why should motion.create usually run outside a component render?

**Answer:** Creating it during render makes a new component type on every render, which can remount the subtree and reset its state.

### Question 2: Which props must a custom wrapped component pass through for Motion to measure it?

**Answer:** The wrapped component should forward its ref and pass Motion props such as style to the DOM element being measured or animated.

### Question 3: How do stable keys help React and Motion?

**Answer:** Stable keys let React preserve the correct component and let Motion match its layout or exit transition.

### Question 4: Why can array indexes cause incorrect list behavior?

**Answer:** An index may point to another item after insertion or reordering, leading to incorrect state preservation or animation.

### Question 5: Which package entry point is intended for Motion components in React Server Components?

**Answer:** The React Server Component entry point is motion/react-client.

### Question 6: When should an interactive component use motion/react?

**Answer:** Use motion/react in an interactive client component that needs state, effects, gestures, or Motion hooks.

### Question 7: What are LazyMotion and m used for?

**Answer:** LazyMotion provides a selected feature bundle, while m is the lighter component API that uses features provided by LazyMotion.

### Question 8: Why should the feature bundle match the animations actually used?

**Answer:** A smaller bundle may omit a needed feature, so the selected bundle must include all animations and interactions used.

## 16. [16. Performance, testing, and release checks](./16-performance-testing-and-release-checks.md)

### Question 1: Why are transform and opacity often good choices for frequent animation?

**Answer:** Browsers can often animate transforms and opacity without recalculating full page layout, which can reduce rendering work.

### Question 2: When might animating width or height be appropriate?

**Answer:** A small, occasional size change may be appropriate when the design needs content to expand naturally, provided it performs well with real content.

### Question 3: Why should off-screen or unnecessary effects be avoided?

**Answer:** They consume resources without helping the current interaction and can distract or affect devices with limited capacity.

### Question 4: Which input methods should be tested for an interactive animation?

**Answer:** Test mouse, keyboard, and touch when those input methods apply to the feature.

### Question 5: What should be checked at narrow and wide viewport sizes?

**Answer:** Check wrapping, measured layout, control access, and motion behavior at both narrow and wide sizes.

### Question 6: How can reduced-motion behavior be verified?

**Answer:** Enable the operating system or browser reduced-motion setting and inspect that the major movement is removed or softened.

### Question 7: Which browser performance signals can help identify animation problems?

**Answer:** Look for dropped frames, long tasks, layout shifts, and rendering work during the actual interaction.

### Question 8: What should be confirmed before releasing a page that uses LazyMotion?

**Answer:** Confirm the production build includes the LazyMotion feature bundle that supplies every animation and gesture the page uses.

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: All code samples](./98-all-code-samples.md) | [Notes index](../README.md) | End of notes |
