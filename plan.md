# Plan: align Vue styling in `src/` with `example-code/`

## Goal
Update styling in the `.vue` files under `src/` to match the TailwindCSS + DaisyUI patterns demonstrated in `example-code/renderer.tsx` and `example-code/build-layout.tsx`.

## 1) Establish the styling baseline (from `example-code`)
- Use DaisyUI theme variables and backgrounds:
  - Page background: `bg-base-200`
  - Surfaces: `bg-base-100`, `bg-base-300`
- Use standard layout primitives:
  - Full-height shell: `min-h-screen flex flex-col`
  - Main content container: `container mx-auto px-4 py-8`
- Use DaisyUI components and variants consistently:
  - Navbar: `navbar bg-base-100 shadow-lg`
  - Buttons: `btn`, `btn-primary`, `btn-outline`, `btn-sm`, `btn-ghost`
  - Alerts: `alert alert-success`, `alert alert-error`
  - Footer: `footer footer-center p-4 bg-base-300 text-base-content`
- Use `data-testid` in kebab-case, with `*-action` naming for clickable actions.

## 2) Inventory what exists today in `src/`
- Enumerate all `.vue` files under `src/` and categorize screens/components:
  - App shell / layout components
  - Navigation
  - Forms
  - Lists / tables
  - Alerts / toasts / error states
- Identify any styling sources that are not aligned (custom CSS in `src/style.css`, ad-hoc Tailwind classes, non-DaisyUI UI patterns).

## 3) Implement a shared Vue layout wrapper
- Create a layout component (e.g. `src/components/AppLayout.vue`) that mirrors `useLayout`:
  - Navbar with left “brand” link and right-side actions area
  - Optional “message” and “error” alert slots/props
  - Main content wrapper: `container mx-auto px-4 py-8`
  - Footer with `bg-base-300 text-base-content`
- Update top-level routing/views to render inside this layout.

## 4) Normalize page-level styling across views
- Ensure the root application provides:
  - `min-h-screen bg-base-200`
- For each view:
  - Replace custom wrappers with `container ...` pattern
  - Use DaisyUI surfaces (`card`, `bg-base-100`, etc.) where appropriate

## 5) Normalize forms and actions
- Buttons:
  - Primary actions: `btn btn-primary`
  - Secondary actions: `btn btn-outline`
  - Compact actions: `btn btn-outline btn-sm`
- Forms:
  - Apply DaisyUI form classes (`input`, `select`, `textarea`, `form-control`, etc.) consistently
  - Ensure edit forms use `value` (not `defaultValue`) where defaults are needed
  - Implement client-side validation using HTML attributes (`required`, `maxlength`, `pattern`, etc.)

## 6) Reduce/centralize custom CSS
- Prefer Tailwind + DaisyUI utility/component classes.
- Keep `src/style.css` limited to:
  - Tailwind directives
  - Small global overrides only if absolutely needed for parity

## 7) Verify and iterate
- Visual check in dev server for:
  - Consistent backgrounds and spacing
  - Navbar/footer alignment
  - Alerts rendering
  - Button/form consistency
- Run Playwright tests; if styling changes affect selectors, add/adjust `data-testid` attributes rather than relying on text/CSS selectors.
