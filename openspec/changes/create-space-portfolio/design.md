# Design

## Context

The repository currently contains OpenSpec setup but no application source or package manifest. The supplied Figma reference is a space-themed work-experience frame with a planetary background, outlined heading, experience details, and keyboard/scroll cues. Its visible "Microsoft SDE Intern" copy is design sample content and is not verified portfolio biography. See proposal.md and the capability specs for motivation and behavior.

## Goals / Non-Goals

**Goals:**
- Start with a maintainable Next.js App Router foundation, TypeScript, and Tailwind CSS.
- Keep portfolio content easy to replace without coupling it to animation or layout components.
- Reproduce the supplied visual direction responsively, with motion that respects reduced-motion preferences.
- Keep the initial site self-contained, with no account or backend dependency.

**Non-Goals:**
- Editing portfolio content through an admin interface or remote CMS.
- Recreating any uninspected Figma frames or treating sample biography copy as verified user data.
- Requiring WebGL, a continuously running animation loop, or external hot-linked artwork for the space scene.

## Decisions

- **Use the Next.js App Router with TypeScript.** Keep the page shell and static portfolio content server-rendered where practical, and isolate interactive section navigation and animation in client components. This avoids making the whole application client-only while preserving browser interaction where needed.
- **Use Tailwind CSS with a small set of theme tokens for the cosmic palette, typography, spacing, and responsive breakpoints.** Keep visual choices consistent across sections and use semantic HTML rather than styling-only controls.
- **Keep portfolio entries in typed local content data.** Components consume explicit experience and section records instead of embedding biography text inside layout markup. Use owner-verified portfolio copy and assets; treat the visible Figma organization and date text as reference/sample data until confirmed.
- **Use the Motion React library for section transitions, with CSS for decorative effects.** A React-aware motion library keeps transitions declarative and tied to section state; CSS handles static stars, gradients, and simple ambient decoration without a canvas animation loop. Disable or substantially reduce non-essential transitions when `prefers-reduced-motion` is active. Keep navigation usable independently of animation completion.
- **Use semantic section anchors and accessible navigation controls.** Let visitors navigate with buttons/links and the keyboard, maintain visible focus, and keep section content in a predictable document order. Avoid global keyboard shortcuts while focus is in an interactive control.
- **Use local, optimized artwork assets.** Export or create the necessary design imagery under the project assets directory instead of depending on remote URLs that can change or fail. Provide a visual fallback so text and navigation remain usable when decorative artwork is unavailable.

## Risks / Trade-offs

- [Only one Figma frame was inspectable, so the complete section inventory and layout are not confirmed] → Before implementing the full portfolio, inspect the remaining frames and reconcile the section list and interactions with the owner; do not invent unverified biography content.
- [Large planetary artwork can increase page weight] → Optimize exported assets, use responsive image sizing, and avoid loading off-screen decorative assets eagerly.
- [Motion can reduce readability or accessibility] → Keep transitions short, retain stable content structure, honor reduced-motion preferences, and never make navigation dependent on animation.
- [The Figma design uses dark, detailed artwork behind text] → Verify foreground contrast at mobile and desktop sizes and preserve readable text if artwork fails to load.
