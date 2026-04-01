# Sources & Influences

Tracks where ideas in this registry came from, what was adapted, and when. Useful for tracking upstream changes, giving credit, and understanding the lineage of each skill.

## Skills

### brainstorming

| Source | What was drawn | Link |
|---|---|---|
| obra/superpowers | Socratic one-question-at-a-time pattern, hard gate on implementation, spec self-review checklist | [skills/brainstorming/SKILL.md](https://github.com/obra/superpowers) |
| EveryInc/compound-engineering-plugin | Scope assessment (Lightweight/Standard/Deep), multiple-choice preference, approach exploration with pros/cons | [ce:brainstorm](https://github.com/EveryInc/compound-engineering-plugin) |
| gsd-build/get-shit-done | Assumptions mode (AI proposes, user corrects), gray area extraction | [discuss-phase](https://github.com/gsd-build/get-shit-done) |

### persistent-planning

| Source | What was drawn | Link |
|---|---|---|
| OthmanAdi/planning-with-files | Three-file pattern (plan/findings/progress), 2-action rule, five-question reboot check, "Context = RAM, Filesystem = Disk" framing | [skills/planning-with-files](https://github.com/OthmanAdi/planning-with-files) |
| gsd-build/get-shit-done | Context budget thresholds (0-30% peak, 50-70% degrading, 70%+ stop), fresh context per executor, wave-based execution | [agents/gsd-executor](https://github.com/gsd-build/get-shit-done) |

### spec-driven-dev

| Source | What was drawn | Link |
|---|---|---|
| github/spec-kit | Constitution concept, phase-gated workflow, spec adherence as a practice | [spec-driven.md](https://github.com/github/spec-kit) |
| Fission-AI/OpenSpec | Delta-based brownfield specs (ADDED/MODIFIED/REMOVED), archive pattern, artifact dependency graph | [docs/concepts.md](https://github.com/Fission-AI/OpenSpec) |
| gotalab/cc-sdd | EARS requirement format, steering/brownfield analysis, gap validation | [spec-requirements.md](https://github.com/gotalab/cc-sdd) |

### compound-learning

| Source | What was drawn | Link |
|---|---|---|
| EveryInc/compound-engineering-plugin | Compound step methodology, bug-track vs knowledge-track formats, overlap detection, three review questions | [ce:compound](https://github.com/EveryInc/compound-engineering-plugin) |
| every.to/guides/compound-engineering | 50/50 rule (features vs system improvement), "each unit of work should make subsequent units easier" philosophy | [Compound Engineering](https://every.to/guides/compound-engineering) |

### frontend-taste (experimental)

| Source | What was drawn | Link |
|---|---|---|
| pbakaus/impeccable | Anti-pattern categories (typography, color, spatial, motion, interaction), reference file architecture, /audit pattern | [impeccable.style](https://github.com/pbakaus/impeccable) |
| Leonxlnx/taste-skill | AI Slop Test concept, bias-correction framing, anti-laziness output concerns | [taste-skill](https://github.com/Leonxlnx/taste-skill) |
| zanwei/design-dna | Design DNA extraction (tokens/style/effects), reference-to-spec pipeline | [design-dna](https://github.com/zanwei/design-dna) |
| OpenAI developers blog | Constraint prompting pattern, narrative sequencing, Playwright verification loop | [Designing delightful frontends](https://developers.openai.com/blog/designing-delightful-frontends-with-gpt-5-4) |

### parallel-agents (experimental)

| Source | What was drawn | Link |
|---|---|---|
| EveryInc/compound-engineering-plugin | Parallel reviewer personas with confidence gating, merge/dedup pipeline, severity scale | [ce:review](https://github.com/EveryInc/compound-engineering-plugin) |
| obra/superpowers | Subagent-driven development, worktree-based isolation | [skills/dispatching-parallel-agents](https://github.com/obra/superpowers) |
| gsd-build/get-shit-done | Wave-based execution, fresh context per executor, orchestrator budget rule (15%) | [agents/gsd-executor](https://github.com/gsd-build/get-shit-done) |

## Landscape reviewed but not adopted (yet)

These were evaluated during the April 2026 landscape review. Documented here for future reference.

| Repo/resource | Why not adopted | Revisit when |
|---|---|---|
| anthropics/skills | Official skill format reference; no workflow content to adapt | Watching for new workflow skills |
| openai/skills | Three-tier promotion model (.system/.curated/.experimental) is a useful reference for csaw's Phase 3 lifecycle | csaw v0.3 promotion design |
| microsoft/skills | Azure-specific domain skills; good multi-agent installer pattern | If adding cloud-provider skills |
| trailofbits/skills | Deep security skills (30+ plugins); trophy case pattern | If expanding security-review depth |
| antfu/skills | Doc-to-skill generation pipeline using git submodules | If adding auto-generation to csaw |
| github/spec-kit | Extension/preset system for spec customization | If spec-driven-dev needs extensibility |
| planning-with-files | Hook-driven enforcement (PreToolUse, PostToolUse, Stop) | When csaw supports hook mounting |
| slavingia/skills | Methodology-as-skills pattern (10 focused skills > 1000 generic) | Philosophy validation, no content to port |
| alirezarezvani/claude-skills | Regulatory/compliance skills (FDA, MDR, ISO 13485, GDPR) | If users need compliance workflows |
| rohitg00/skillkit | Closest csaw competitor; copies vs symlinks, 44-agent support | Competitive awareness |
| caliber-ai-org/ai-setup | LLM-generates config files; scoring/audit pattern | Complementary tool, not competing |
| cisco-ai-defense/skill-scanner | Security scanner for skills; SARIF output for CI | Potential csaw integration (csaw scan) |
| memodb-io/Acontext | Memory-as-skill-files pipeline; progressive disclosure retrieval | If csaw adds memory/learning features |

## How to update this document

When adapting ideas from a new source:
1. Add a row to the relevant skill's table with the source, what was drawn, and a link.
2. If the source was reviewed but not adopted, add it to the landscape table with rationale.
3. Date significant reviews (like this one: April 2026 landscape review).
