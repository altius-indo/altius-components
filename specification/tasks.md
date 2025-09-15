# Coding Tasks

## App Navigation UI
- Implement sticky top bar with centered logo linking to home.
- Add burger menu button to toggle left slide-in navigation panel.
- Build navigation panel with composable item components, section grouping, and close on outside click or `Esc`.
- Show authentication state in right corner: login button when logged out, avatar with popover (Preferences, Account, Log out) when logged in.
- Include three-dot settings trigger routing to settings page or panel.
- Ensure theming support and responsive behavior (mobile full-screen panel, desktop ~320px width).

## Component Library Infrastructure
- Organize components under `src/lib/components/<Component>/` with implementation, `index.ts`, stories, and tests.
- Provide shared utilities in `src/lib/utils/` (e.g., `cn`, types helpers).
- Style components using Tailwind CSS, Skeleton plugin, and `tailwind-variants` for variants.
- Set up Storybook stories (`Component.stories.ts`) and Vitest unit tests (`Component.test.ts`).
- Configure Playwright E2E tests in `e2e/` and run via `npm test`.
- Bundle library with `svelte-package`; re-export modules from root `index.ts`.

## Product Roadmap
- Integrate Skeleton default theme and wrap base components.
- Implement ThemeProvider store with runtime light/dark switching and custom theme support.
- Expand component set: Button, Input, Select, Modal, Toast, Tabs, Accordion, Navbar.
- Write Storybook MDX guides, interactive stories, and autodocs.
- Add unit tests per component and expand Playwright scenarios for complex interactions.
- Configure CI/CD pipeline: lint → unit tests → build → Storybook deploy, optional Chromatic visual regression.
