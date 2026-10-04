# 16. Performance, testing, and release checks

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: React patterns and bundle choices](./15-react-patterns-and-bundle-choices.md) | [Notes index](../README.md) | [Next: All code samples](./98-all-code-samples.md) |

## Animate properties that stay smooth

Transforms and opacity are usually efficient properties to animate because browsers can often update them without recalculating the full page layout. Prefer x, y, scale, rotate, and opacity for frequent motion when they express the design clearly.

Animating width, height, top, or left can trigger layout work. That may still be the right choice for a small, occasional transition, but test it with realistic content and slower devices. A smooth result on a short example does not prove a large page will stay smooth.

## Keep animation work focused

Animate only the elements that need to change. Avoid running a continuous animation when the user cannot see the element, and avoid measuring or updating React state on every frame when a Motion value can drive the visual property directly.

Use layout animation for meaningful layout changes and use reduced-motion preferences for movement that could be uncomfortable. Remove effects that do not improve feedback or understanding.

## Test real interactions

Check the feature with mouse, keyboard, and touch when those inputs apply. Confirm buttons still work, focus remains visible, exit states complete, list keys remain stable, and scroll animations behave inside the intended container.

Test at narrow and wide viewport sizes. Content length, font loading, and responsive layout can change measured positions and expose animation issues that a fixed desktop example hides.

## Verify reduced motion and initial rendering

Enable the operating system's reduced-motion preference and inspect the most noticeable movement. Confirm that important information remains visible and that no interaction depends on an animation finishing before the user can continue.

For server-rendered pages, check the initial HTML and hydration in the browser console. Avoid reading browser-only values during server rendering. If a component should not animate its server-rendered initial state, consider initial={false} and verify the expected behavior after hydration.

## Measure before optimizing

Use browser performance tools to inspect dropped frames, long tasks, layout shifts, and rendering work during the actual interaction. Compare the page with and without an effect when its cost is unclear.

If bundle size matters, inspect the production build and choose a LazyMotion feature bundle that covers the components in use. Keep source maps and development diagnostics separate from production decisions according to the project build setup.

## Release checklist

Before publishing an animated interface, confirm that the feature works with reduced motion, keyboard focus is visible, touch interactions do not block normal scrolling, the page remains usable without animation, list items have stable keys, and the production build includes the needed Motion features.

Document any browser-specific issue with a small reproducible example. A focused example is easier to test and maintain than a large component with several unrelated effects.

## Practice questions

1. Why are transform and opacity often good choices for frequent animation?
2. When might animating width or height be appropriate?
3. Why should off-screen or unnecessary effects be avoided?
4. Which input methods should be tested for an interactive animation?
5. What should be checked at narrow and wide viewport sizes?
6. How can reduced-motion behavior be verified?
7. Which browser performance signals can help identify animation problems?
8. What should be confirmed before releasing a page that uses LazyMotion?

## Main references

- [Motion component performance](https://motion.dev/docs/react-motion-component)
- [Layout animation](https://motion.dev/docs/react-layout-animations)
- [Accessibility and reduced motion](https://motion.dev/docs/react-accessibility)
- [LazyMotion](https://motion.dev/docs/react-lazy-motion)