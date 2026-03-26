---
name: react-patterns
description: React component and performance patterns. Use when writing, reviewing, or refactoring React components.
---

# React Patterns

## When to use

- Building React components
- Reviewing React PRs for performance issues
- Refactoring class components or legacy patterns
- Optimizing renders and bundle size

## Guidelines

### Components

- Functional components only. No class components in new code.
- One component per file for anything non-trivial.
- Co-locate styles, tests, and types with the component.
- Prefer composition over prop drilling. Use context sparingly and for truly global state.

### State management

- `useState` for local UI state.
- `useReducer` for complex state transitions.
- Server state belongs in a data fetching library (React Query, SWR), not local state.
- Derive values during render — don't sync state with effects.

### Performance

- Don't optimize renders prematurely. Measure first.
- Use `React.memo` only when profiling shows unnecessary re-renders.
- Use `useMemo` / `useCallback` for expensive computations or stable references passed to memoized children.
- Split heavy components behind `React.lazy` + `Suspense`.
- Avoid defining components inside other components — creates new instances every render.

### Data fetching

- Fetch on the server when possible (RSC, getServerSideProps, loader).
- Use Suspense boundaries to stream content progressively.
- Parallelize independent fetches with `Promise.all`, not sequential awaits.
- Cache and deduplicate with SWR or React Query, not manual state.

### Forms

- Use controlled inputs for simple forms.
- Use a form library (React Hook Form, Formik) for complex multi-field forms.
- Validate on blur for UX, on submit for correctness.
- Never trust client-side validation alone — validate server-side too.

## Anti-patterns

- Don't use `useEffect` for derived state — compute during render.
- Don't use `useEffect` for event handling — use event handlers.
- Don't spread unknown props onto DOM elements — pick explicitly.
- Don't suppress ESLint exhaustive-deps warnings — fix the dependency array.
- Don't use `index` as key for lists that reorder or mutate.
