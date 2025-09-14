# Product Specification: SvelteKit Component Library with Tailwind & Skeleton

## 1. Vision & Goals
Build a reusable, themable Svelte component library that:
- Ships modular UI primitives and composite widgets.
- Supports light/dark themes with runtime switching.
- Uses [Skeleton for Svelte](https://www.skeleton.dev/) for layout primitives and typography.
- Exposes documented components via Storybook.
- Enforces quality with TypeScript, unit tests, and Playwright E2E checks.
- Packages as an npm-ready module.

## 2. Repository Structure
- `src/lib`: core component source, helpers, and type utilities.
  - `utils.ts` hosts class/prop helpers (`cn`, `WithoutChild`, `WithElementRef`, etc.)
  - `index.ts` re-exports published components.
- `src/routes`: SvelteKit demo site and integration playground; shows component usage (e.g., `<Button/>`)
- `src/stories`: Storybook stories and demo components (e.g., `Button.stories.svelte`)
- `e2e`: Playwright tests verifying basic page rendering
- Root configs: Tailwind theme tokens and typography in `tailwind.config.js`, SvelteKit aliases in `svelte.config.js`, and scripts in `package.json`.

## 3. Technology Stack
| Concern | Technology |
|--------|------------|
| Framework | SvelteKit |
| Styling | Tailwind CSS 4 + Skeleton for Svelte |
| Theming | CSS variables + Tailwind tokens |
| Docs | Storybook (SvelteKit integration) |
| Testing | Vitest unit tests, Playwright E2E |
| Packaging | `@sveltejs/package` via `npm run prepack` |

## 4. Component Architecture
### 4.1 Design Principles
- Components are authored in Svelte using Tailwind utility classes.
- Shared class merging through `cn()` ensures predictable class composition.
- Props should omit `child/children` unless explicitly required (`WithoutChildrenOrChild` types).
- Each component exports a typed Svelte component plus an index file for tree-shakable imports (`src/lib/components/<component>/index.ts`).

### 4.2 Skeleton Integration
- Import Skeleton base styles and layout primitives at app bootstrap.
- Utilize Skeleton’s design tokens (spacing, typography) as defaults, extending them via Tailwind’s `theme.extend` to align with brand colors and fonts.
- Wrap low-level Skeleton elements (e.g., `Button`, `Card`, `Tabs`) with library-specific APIs for consistent variant/size props.

### 4.3 Component Examples
- **Button**
  - Variants: primary, secondary, outline, ghost.
  - Sizes: sm, md, lg, full-width.
  - Composition: uses Skeleton’s `Button` base, extended via Tailwind classes and `cn()`.
  - Stories: interactive examples in Storybook demonstrating all variants and controlled props.
- **Input Field**
  - Integrated with Skeleton’s form styles.
  - Supports validation states (success, error) using theme colors (`success` and `error` palettes in Tailwind config).
- **Modal, Tooltip, Tabs, Toast**
  - Compose Skeleton primitives; provide accessibility attributes and cross-theme styling.

## 5. Theming & Dark Mode
### 5.1 Theme Tokens
- The Tailwind configuration defines brand, neutral, and semantic palettes.
- Fonts, spacing, shadows, and radii extend Tailwind defaults for a consistent design system (e.g., `borderRadius` values).

### 5.2 Runtime Theme Switching
- Use CSS variables for primary palette and semantic colors.
- Implement a `<ThemeProvider>` Svelte store to toggle `data-theme="light|dark"` at the root element.
- Tailwind’s `dark` variant toggles based on `class="dark"`; adapt Skeleton’s themes by updating the `<html>` class.

### 5.3 Custom Themes
- Provide CLI or config-driven theme definitions that merge custom palettes into Tailwind config.
- Allow components to read theme tokens via CSS variables to avoid recompilation for theme changes.

## 6. Storybook Integration
- Uses `@storybook/sveltekit` with SvelteCSF and Vitest addons.
- Stories reside in `src/stories`, following CSF syntax (`defineMeta`, `Story`) for auto-generated docs.
- Add Chromatic or VRT workflows for visual regression.
- Provide global decorators for theme switching and Skeleton layout.

## 7. Testing Strategy
### 7.1 Unit & Component Tests
- Vitest for logic and Svelte components (`npm run test:unit`).
- Include browser-mode testing (`vitest-browser-svelte`) for DOM events.
- Example: ensure `<Button>` renders proper classes and handles `onClick`.

### 7.2 End-to-End Tests
- Playwright suite under `e2e/` with basic navigation check.
- Expand tests for components that rely on global theming or multi-step interactions.

### 7.3 Linting & Type Safety
- `svelte-check` and TypeScript compile in CI (`npm run check`).

## 8. Build & Distribution
- `npm run prepack` generates distributable package with `svelte-package` and `publint` checks.
- Output (`dist/`) includes bundled JS, type declarations, and pruned tests.
- Components can be consumed via `import { Component } from 'altius-components'`.

## 9. Roadmap
1. **Skeleton Integration**
   - Configure Skeleton default theme; wrap base components.
2. **Theming API**
   - Implement ThemeProvider store, expose `useTheme()` hook.
   - Provide default light/dark themes and CLI/JSON config for custom themes.
3. **Component Expansion**
   - Build core set: Button, Input, Select, Modal, Toast, Tabs, Accordion, Navbar.
4. **Documentation**
   - Write Storybook MDX guides and interactive stories.
   - Generate API docs via autodocs.
5. **Testing Enhancements**
   - Add unit tests per component; snapshot styles for theming.
   - Expand Playwright scenarios for complex flows (modal open/close, tab switching).
6. **CI/CD**
   - GitHub Actions: lint → unit tests → build → Storybook deploy.
   - Optional Chromatic integration for visual regression.
