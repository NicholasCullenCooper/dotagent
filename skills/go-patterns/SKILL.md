---
name: go-patterns
description: Go idioms and patterns for writing clean, idiomatic Go. Use when writing, reviewing, or refactoring Go code.
---

# Go Patterns

## When to use

- Writing new Go code
- Reviewing Go PRs
- Refactoring Go toward idiomatic patterns

## Guidelines

### Error handling

- Always wrap errors with context: `fmt.Errorf("doing thing: %w", err)`
- Return errors, don't panic. Reserve panic for truly unrecoverable programmer bugs.
- Check errors immediately after the call. No deferred error checking.
- Use `errors.Is` and `errors.As` for error inspection, not string matching.

### Naming

- Short variable names for small scopes: `r` for a reader in a 5-line function.
- Descriptive names for exported symbols and wider scopes.
- Interfaces named by what they do: `Reader`, `Stringer`, not `IReader`.
- Package names are lowercase, single word, no underscores.

### Concurrency

- Start goroutines only when there's a clear owner that waits for completion.
- Use `context.Context` for cancellation, not channels-of-channels.
- Prefer `sync.WaitGroup` over manual done channels for fan-out.
- Never start a goroutine without a clear shutdown path.

### Project structure

- Prefer `internal/` for non-exported packages.
- Keep `main` packages thin — parse flags, wire dependencies, call into libraries.
- Use interfaces at consumption sites, not declaration sites.
- Avoid premature abstraction. Three duplications before extracting.

### Testing

- Table-driven tests with `t.Run` subtests.
- Use `t.TempDir()` for filesystem tests, not manual cleanup.
- Test behavior, not implementation. Mock at boundaries, not internally.
- Use `t.Helper()` in test helper functions.

## Anti-patterns

- Don't use `init()` for anything other than registering drivers.
- Don't use package-level variables for mutable state.
- Don't use `interface{}` / `any` when a concrete type or generic will do.
- Don't return `(result, error)` where error is always nil.
- Don't use `go test -count=1` in CI — fix flaky tests instead.
