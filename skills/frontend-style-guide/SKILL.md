---
name: frontend-style-guide
description: Applies this repository's frontend naming, folder structure, import/export, React, and TypeScript conventions. Use when creating or refactoring frontend files, placing components/hooks/utils, reviewing frontend code style, or deciding `src/pages` vs `src/common` placement.
---

# Frontend Style Guide

Operational rules for frontend structure and naming in this repo.

For rationale, extended examples, and migration notes, read [frontend/docs/frontend-style-guide.md](../../frontend/docs/frontend-style-guide.md).

## Placement Workflow

Before creating a file, decide where it belongs:

1. **Page-specific?** → `src/pages/<page>/components|hooks|utils/`
2. **Used by 2+ pages?** → `src/common/components|hooks|utils|store/`
3. **Route definition?** → `src/router/`
4. **Generated API client?** → `src/api/` (never edit by hand)
5. **Theme tokens/providers?** → `src/theme/`

When unsure, start page-local; promote to `common/` only after reuse is clear.

## New File Checklist

- [ ] Correct folder (`pages` vs `common`)
- [ ] Correct casing (`PascalCase.tsx` vs `camelCase.ts`)
- [ ] Named export (no default unless routing/lazy constraints require it)
- [ ] No barrel `index.ts` unless small and explicit
- [ ] User-visible strings use `useTranslation()` + keys in `public/locales/en/` and `public/locales/hu/`
- [ ] Tests for non-trivial behavior; stories for reusable UI

## Quick Rules

- Use page-first colocation. Keep page-specific code near the page.
- Use named exports by default.
- Use `PascalCase` for React component files.
- Use `camelCase` for non-component files.
- Do not use barrel exports by default.
- Keep business logic out of presentational components when practical.

## File Naming

### Components

- File names: `PascalCase.tsx`
- Component names: `PascalCase`
- Props type names: `ComponentNameProps`

Examples:

- `src/pages/chat/components/ChatShell.tsx`
- `src/common/components/ui/Button.tsx`

### Hooks

- File names: `useSomething.ts` or `useSomething.tsx`
- Hook names: `useSomething`
- Prefer object return values for custom hooks

### Non-component files

- File names and function names: `camelCase`
- Boolean names: `is*`, `has*`, `can*`, `should*`

Examples:

- `src/common/utils/fetchSse.ts`
- `src/common/store/uiStore.ts`

### Tests and stories

- Tests: `ComponentName.test.tsx` or `something.test.ts`
- Stories: `ComponentName.stories.tsx`

## Folder Placement

Use this structure:

- `src/pages/<page>/...` for page-specific components/hooks/utils
- `src/common/...` for shared code reused by multiple pages
- `src/router/` for route definitions
- `src/api/` for generated API client code only
- `src/theme/` for theme setup/tokens/providers
- `src/test/` for test setup/utilities

Rules:

- Move code to `src/common/` only after reuse is clear.
- Keep route definitions in `src/router/`.
- Never manually edit generated code under `src/api/`.

## Exports and Imports

- Prefer named exports.
- Avoid default exports unless routing/lazy constraints require them.
- No barrel files by default.
- Exception: allow a small, explicit local `index.ts` when justified.
- No wildcard `export *` from broad trees.
- Use short relative imports inside the same page module.
- Use aliases (for example `@/`) for cross-page/common imports.
- Avoid deep relative paths when readability suffers.

## React Conventions

- Functional components only.
- Keep components focused; split when handling multiple concerns.
- Prefer early returns for loading/error branches.
- Suggested order inside component bodies:
  1. Hooks and derived values
  2. Effects
  3. Event handlers and helpers
  4. Returned JSX
- Event props use `onX`; local handlers use `handleX`.

## TypeScript Conventions

- Favor type inference unless explicit annotations improve correctness.
- Avoid `any`; use `unknown` with narrowing.
- Prefer discriminated unions over optional-field/flag-heavy shapes.
- Keep properties required by default; add optional fields deliberately.
- Use `as const` and `satisfies` where they improve safety.
- Prefer `import type` for type-only imports.
- Avoid unsafe assertions (`as Foo`, `value!`) unless justified.
- Use `type` by default; use `interface` when extension/merging clearly helps.

## State and Data Flow

- Server state: TanStack Query generated hooks.
- Global UI state: Zustand only when state is truly global.
- Prefer URL state for shareable filters/sort/navigation state.
- Pass only required props to children.

## Testing and Storybook

- Add tests for non-trivial behavior and state transitions.
- Add stories for reusable UI components.
- Keep tests close to implementation when practical.
- Test behavior/outcomes, not framework internals.

## i18n Requirement

- Wrap user-visible strings with `useTranslation()` from `react-i18next`.
- Add translation keys to both `public/locales/en/` and `public/locales/hu/`.

## Do / Don't

Do:

- `src/pages/chat/components/ChatMessageList.tsx`
- `src/pages/chat/hooks/useChatStream.ts`
- `src/common/utils/formatTimestamp.ts`
- `src/common/components/ui/Button.tsx`

Don't:

- `src/common/components/chat-message-list.tsx` (component file must be `PascalCase`)
- `src/pages/chat/hooks/UseChatStream.ts` (non-component file must be `camelCase`)
- Broad wildcard re-exports through `index.ts`
- `src/utils.ts` for page-specific logic that should live under a page

## Migration Rule

- Apply these conventions to all new files immediately.
- Migrate existing files incrementally when touching them.
- Avoid broad rename-only refactors unless explicitly requested.
- If generated code conflicts with conventions, leave generated code unchanged and adapt surrounding code.
