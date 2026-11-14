---
name: "kiss"
description: "Prevent AI-generated over-engineering and hard-to-read code during software design, implementation, refactoring, and code review. KISS (Keep It Simple, Stupid): use when choosing or designing an architecture, writing or changing code, reviewing a diff, naming symbols, reducing boilerplate, or when the user asks for simple, minimal, boring, discoverable, human-readable code."
version: 1
created: "2026-08-15"
updated: "2026-08-22"
---
## When to Use
Use for software design, implementation, refactoring, debugging, naming, and review. KISS means choosing the smallest clear solution that satisfies current requirements, not minimizing characters or sacrificing correctness.

Always load communication and output guidance: [references/communication.md](references/communication.md).

Also load each relevant task playbook once:

- Design or architecture: [references/design.md](references/design.md)
- Writing, fixing, or refactoring code: [references/coding.md](references/coding.md)
- Reviewing a design or code change: [references/review.md](references/review.md)

## Non-Negotiable Boundaries
Readability, low cognitive load, and human debugging are requirements. A maintainer must be able to trace execution, inspect state, set breakpoints, and connect failures to their source without decoding clever compression, hidden control flow, surprising language tricks, or metaprogramming.

Never simplify away correctness, explicit requirements, trust-boundary validation, security, data-loss prevention, accessibility, required error handling, or operational observability. Fix root causes at the narrowest shared owner after checking callers and sibling paths.

Add abstractions only for current duplication or variation when they make the system easier to understand. Do not build for hypothetical futures.

If the user explicitly requests a structure these playbooks reject (a service, framework, plugin system, or configuration point), name the simpler alternative and its trade-off, then let the user decide. Do not silently comply or silently refuse.

## Output Contract
Deliver the requested artifact first. Keep commentary concise and professional. State material simplifications or deferred capabilities only when they affect behavior, risk, or a future decision. Preserve exact identifiers, commands, error strings, numbers, and units.

Follow its task-specific output shape. Do not add an essay defending simplicity.

## Sources and License

This skill synthesizes ideas from `write-discoverable-code`, `ponytail`, and `caveman`, all MIT-licensed. See [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).