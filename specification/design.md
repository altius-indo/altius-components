# Low-Level Design: SvelteKit Component Library

## Directory Structure
- `src/lib/components/<Component>/` – each component lives in its own folder.
- `src/lib/components/<Component>/<Component>.svelte` – component implementation.
- `src/lib/components/<Component>/index.ts` – export entry.
- `src/lib/utils/` – shared utilities.
- `src/routes/` – demo and integration playground.

## Component Anatomy
- Props declared with `export let` and typed via TypeScript.
- Slots expose custom content; default slot for markup.
- Events dispatched using `createEventDispatcher`.
- Each component exports an interface for public API.

## Styling
- Tailwind CSS provides base styling and tokens.
- Theme configuration lives in `tailwind.config.js`.
- Components leverage the Skeleton plugin and `tailwind-variants` for variants.

## Documentation and Testing
- Storybook stories reside alongside components (`Component.stories.ts`).
- Unit tests written with Vitest (`Component.test.ts`).
- End-to-end tests executed with Playwright in `e2e/`.
- `npm test` runs unit and e2e suites.

## Packaging
- `svelte-package` bundles the library into `dist/`.
- Root `index.ts` re-exports all component modules.
