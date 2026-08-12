# Design system and UX rules

- Tailwind CSS is the base system. Only design tokens defined here; no raw hex values in components.
- Semantic colors: success, warning, danger, info - never reused for decoration.
- Responsive: every screen usable at 360px, 768px and 1280px widths.
- Loading, empty and error states are part of every screen specification - a screen
  without them is not finished.
- Destructive actions require confirmation and are never the default button.
- The first render of a new screen is the first design review: look at the running
  application before iterating.
