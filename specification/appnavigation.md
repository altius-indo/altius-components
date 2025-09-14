# App Navigation UI Specification

## 1. Top Bar Structure
- A sticky top bar spans the width of the viewport and remains visible during scroll.
- The app logo is centered within the bar; clicking it navigates to the home route.
- **Left Corner:** a burger menu button toggles the navigation panel.
- **Right Corner:** display (from left to right) the user avatar and a three‑dot settings trigger.

## 2. Burger Menu & Navigation Panel
- Clicking the burger icon opens a modal panel that slides from the left and overlays page content.
- The panel supports scroll and closes when clicking outside or pressing `Esc`.
- Navigation items are composable button‑like components with:
  - optional left icon,
  - text label,
  - optional right icon (chevron, badge, etc.).
- Items emit click/navigation events and expose active and disabled states.
- The panel can group items under titled sections separated by dividers.

## 3. User Avatar & Authentication
- When logged out, show a "Log in" button in place of the avatar.
- After authentication, display the user’s avatar or initials.
- Clicking the avatar opens a popover menu containing:
  - "Preferences" link,
  - "Account" link,
  - "Log out" action.

## 4. Settings Trigger
- A three‑dot icon sits to the right of the avatar.
- Activating it routes to a dedicated Settings page or opens a settings panel.

## 5. Theming & Responsiveness
- The top bar and navigation panel inherit the app’s theme (light/dark).
- Mobile: panel covers the screen; desktop: panel width ~320px.
- Components use accessible semantics (`nav`, `button`, `aria-expanded`).

## 6. Extensibility Notes
- Navigation items accept slots for custom content and are individually importable.
- Sections can be supplied as configuration objects for dynamic menus.
- Icons follow the library’s icon package (e.g., Lucide) and may be replaced via props.

