# Coding Playbook

Apply [communication.md](communication.md) to code comments, implementation summaries, validation results, and limitations.

Write the smallest clear change that fixes the real problem and fits the codebase.

## Core Loop

1. Read the target code and tests, understand the requirement, trace callers and sibling paths, and define what must remain unchanged. In files handling untrusted input, persistence, security, or external calls, list the concrete constraints that must survive before deleting anything: validation codes, trust boundaries, atomicity, timeouts, and retries.
2. Find the root cause and its narrowest shared owner. Prefer deleting or avoiding work before adding a mechanism.
3. Reuse an existing project pattern, then the standard library, native platform or database, then an installed dependency.
4. Add minimal custom code only when those options fail. Require demonstrated benefit for a new dependency or service.
5. Prefer explicit, boring, searchable code with visible state and control flow over clever compression.
6. Run the smallest check that can catch the likely failure.

Small does not mean local: one correction at the shared owner is simpler than duplicated guards in callers.

## Structure Before Behavior

Apply the structure-first invariant from SKILL.md: declare signatures with parameters, return, and errors, plus data shapes and boundaries, before writing bodies; when changing code, change the declaration before the bodies. It applies to functions, types, and modules, not just classes. A declaration does not license an extra layer — interfaces and factories still need current variation. Keep this step internal.

## Code Rules

- Keep the diff focused. Do not mix unrelated cleanup into the change.
- Avoid one-use abstractions, pass-through layers, speculative options, generic wrappers, and future scaffolding. Extract only to name a real concept, remove meaningful duplication, or isolate a necessary boundary.
- Keep related behavior together. Do not create one file per trivial helper.
- Preserve project conventions and familiar language idioms. Isolate required framework mechanics behind a clear boundary.
- Keep state changes and side effects visible. Use named intermediate values when they clarify intent, expose state, or provide useful breakpoints.
- Keep control-flow nesting (loops, conditionals, exception handling, scoped blocks) within two levels; split deeper logic into focused helpers with clear data flow.
- Give each function, class, and logic block a short comment explaining what and why, without narrating individual statements.
- Weave what and why naturally into docstrings and comments; do not add separate `Why:` or `Example:` headings. When examples are needed, cover every language the project uses.
- Keep complete event names, flags, error codes, and diagnostic prefixes as searchable literals.
- Add a dependency only when maintained behavior is materially safer or smaller than owned code, considering transitive cost, security, runtime footprint, and project conventions.

## Agent-Friendly Naming

- Reuse established domain vocabulary. One concept gets one spelling across modules, files, symbols, APIs, tests, logs, and documentation.
- Name modules and files after the concept an agent will search for. Avoid bare `utils`, `helpers`, `types`, `config`, or `handlers`; qualify the role with its domain.
- Give exported functions, classes, and types enough context to search uniquely. Give generic verbs an object: prefer `sanitizeEmailHtml` to `sanitize`.
- Use domain types or branded IDs when primitive arguments could be confused, and model distinct states explicitly instead of hiding rules in nullable fields.
- Keep one definition site per symbol. Rename stale identifiers when behavior or visibility changes, and point deprecated paths to their replacement.
- Use complete searchable literals for errors, events, flags, and diagnostic prefixes. Add a stable error prefix that leads back to its source.
- Add concise API documentation when a signature hides units, timezone, ownership, ordering, or source semantics. Include the natural-language phrase an agent is likely to search for when the identifier alone is insufficient.

## Verification

- Existing behavior: run the narrowest relevant test.
- New branch or loop: add one focused test for behavior and one meaningful edge when needed.
- Bug fix: add a regression check that fails before the fix.
- Money, permissions, security, migration, or data-loss path: do not under-test for brevity.

Prefer a small runnable check over a large fixture framework. Report exactly what ran and whether it passed. Before finishing, remove any added file, layer, option, dependency, or shorter expression that does not earn its cost in current readability, correctness, or diagnosability.
