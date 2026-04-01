---
name: brainstorming
description: Collaborative design refinement through structured questioning before planning or implementation. Use when scoping new work, exploring ambiguous requirements, or stress-testing an idea before committing to a plan.
---

# Brainstorming

## What this is for

Surface ambiguity, explore alternatives, and converge on a design before any code is written. The output is a requirements document — not a plan, not code. Implementation is gated behind explicit design approval.

## When to use it

- Starting new feature work where scope or approach is unclear.
- Enhancing existing behavior where trade-offs need discussion.
- Exploring a problem where the right solution is not yet obvious.
- Any time you would otherwise jump straight to coding something non-trivial.

## When to skip it

- The change is mechanical (rename, dependency bump, config tweak).
- The scope is already well-defined and the implementation path is clear.
- You are executing against an approved plan or spec.

## Gather first

- Existing code, docs, or specs related to the area.
- Any constraints (performance, compatibility, deadlines, dependencies).
- The user's rough intent — even a single sentence is enough to start.

## Workflow

### 1. Assess scope

Before starting a dialogue, classify the work:

| Scope | Signal | Ceremony |
|---|---|---|
| Lightweight | Single file, well-understood change, <30 min | Quick 2-3 question check, inline notes |
| Standard | Multiple files, some ambiguity, new behavior | Full brainstorm with requirements doc |
| Deep | Cross-cutting, multiple stakeholders, new subsystem | Full brainstorm, possibly split into sub-brainstorms |

Match ceremony to scope. Do not force a heavyweight process on a lightweight change.

### 2. Explore context

Read the relevant code and docs. Understand the current state before asking questions. Your first question should demonstrate that you already understand the landscape.

### 3. Ask questions — one at a time

This is the core of the skill. Rules:

- **One question per turn.** Never stack multiple questions.
- **Prefer multiple choice.** Offer 2-3 concrete options with trade-offs rather than open-ended "what do you want?" When the space is genuinely open, say so.
- **Challenge the premise.** If the request has an assumption that seems wrong or costly, name it. "You mentioned X — have you considered that Y would avoid Z?"
- **Surface gray areas.** Actively look for things that are ambiguous, underspecified, or assumed. Name them explicitly: "This is a gray area — here's what I think, but you should weigh in."
- **Propose, don't just ask.** Instead of "how should we handle errors?" say "I'd suggest failing fast with a clear message because [reason] — does that match your expectation, or do you need graceful degradation?"

### 4. Explore approaches

Once the problem is understood, present 2-3 concrete approaches. For each:

- What it looks like in practice (concrete, not abstract).
- Pros — what it buys you.
- Cons — what it costs or risks.
- When you would pick it.

Let the user choose or combine. Do not pick for them unless asked.

### 5. Surface assumptions (optional fast path)

If the codebase is large or the user wants speed: analyze the code first, then present your assumptions with evidence. The user corrects only what is wrong. This typically resolves in 2-4 interactions instead of 15-20 open-ended questions.

Format:
```
Based on [evidence], I'm assuming:
1. [assumption] — because [evidence]
2. [assumption] — because [evidence]
...
Correct anything that's off and I'll adjust.
```

### 6. Write the requirements document

When alignment is reached, produce a document with:

- **Problem frame** — what is being solved and why.
- **Requirements** — numbered, testable statements (R1, R2, ...). Each requirement should be independently verifiable.
- **Scope boundaries** — what is explicitly out of scope.
- **Success criteria** — how you know it worked (technology-agnostic where possible).
- **Key decisions** — choices made during brainstorming and their rationale.
- **Open questions** — split into "resolve before planning" and "defer to planning."

### 7. Self-review the document

Before presenting, check:

- [ ] Every requirement is testable — you could write a pass/fail check.
- [ ] Scope boundaries are explicit — someone could say "that's out of scope" with confidence.
- [ ] No implementation details leaked in — requirements describe behavior, not code.
- [ ] YAGNI applied — nothing is included "just in case."
- [ ] Open questions are honest — you did not paper over ambiguity.

### 8. Get explicit approval

Present the document. Do not proceed to planning or implementation until the user approves or requests changes. This is a hard gate.

## Decision rules

- If the user says "just do it" for something non-trivial, still do a lightweight scope check (step 1). You can compress the process but not skip it entirely.
- If brainstorming reveals the work should be split, propose sub-scopes and brainstorm each.
- Implementation details (file paths, function signatures, libraries) belong in planning, not here — unless the user explicitly brings them up.
- Visual aids are useful for flows and comparisons. Use diagrams for processes, tables for trade-offs. Do not add visuals for decoration.

## Failure modes

- **Asking too many questions at once.** The user gets overwhelmed and gives shallow answers. One question, one turn.
- **Open-ended questions without proposals.** "How should we handle X?" is lazy. "I'd suggest X because Y — agree?" is useful.
- **Skipping brainstorming for "simple" things that aren't.** If you later discover ambiguity during implementation, the brainstorm was needed.
- **Gold-plating the requirements.** The document should be as short as possible while being complete. Two pages beats ten.
- **Proceeding without approval.** The gate exists because building the wrong thing is more expensive than waiting for a response.

## Output

A requirements document. Location and format are flexible — a markdown file in `docs/brainstorms/`, an inline response, or wherever the project convention puts design artifacts. The content matters more than the container.
