---
name: typescript-patterns
description: TypeScript idioms and type safety patterns. Use when writing, reviewing, or refactoring TypeScript code.
---

# TypeScript Patterns

## When to use

- Writing new TypeScript code
- Reviewing TypeScript PRs
- Migrating JavaScript to TypeScript
- Tightening type safety in existing code

## Guidelines

### Type safety

- Enable `strict: true` in tsconfig. No exceptions.
- Use `unknown` over `any` when the type is genuinely unknown.
- Use discriminated unions for state machines and variant types.
- Use `as const` for literal types and exhaustive switch checks.
- Validate external data at boundaries with zod, valibot, or similar. Trust internal types.

### Function design

- Prefer explicit return types on exported functions.
- Use function overloads sparingly — discriminated union params are usually clearer.
- Use `readonly` arrays and objects in function signatures when mutation isn't intended.
- Prefer `type` over `interface` unless you need declaration merging or `extends`.

### Error handling

- Use Result types (`{ ok: true, data } | { ok: false, error }`) for expected failures.
- Reserve `throw` for unexpected/programmer errors.
- Never `catch` and ignore. At minimum, log.
- Type your error handling — `catch (e: unknown)` and narrow.

### Module organization

- One export per concept. Avoid barrel files (`index.ts` re-exports) — they break tree-shaking.
- Co-locate types with the code that uses them.
- Use `import type` for type-only imports.

### Testing

- Prefer integration tests over unit tests for business logic.
- Use vitest or jest with `--typecheck` to catch type errors in tests.
- Test error paths, not just happy paths.
- Mock at boundaries (API clients, databases), not internal modules.

## Anti-patterns

- Don't use `any` to silence the compiler. Fix the type.
- Don't use `!` (non-null assertion) — narrow with a check instead.
- Don't use `enum` — use `as const` objects or union types.
- Don't write `.d.ts` files by hand when you can infer from source.
- Don't suppress `@ts-ignore` without a comment explaining why.
