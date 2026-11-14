# Review Playbook

Apply [communication.md](communication.md) when writing findings, evidence, fixes, and the review summary.

Review for correctness first, then unnecessary complexity, then clarity. Do not confuse a short diff with a correct design.

## Review Order

1. Understand the requirement and trace the changed path end to end.
2. Check correctness, security, data integrity, concurrency, compatibility, and failure behavior.
3. Check tests against likely regressions and edge cases.
4. Evaluate whether a human can trace the path, inspect state, set breakpoints, and diagnose failures without decoding hidden behavior.
5. Look for accidental complexity, unrelated cleanup, and names that prevent an agent from finding a concept, its owner, or its definition with one search.
6. Report only findings that have a concrete impact or a clear simplification.

## Complexity Check

For every new component, abstraction, dependency, configuration option, or layer, ask:

- Which current requirement needs it, and what breaks if it is removed?
- Does the project, standard library, platform, or installed dependency already provide it?
- Is there current duplication or variation, or only a prediction?
- Does it make ownership, data flow, and the common path easier to understand?

Flag one-implementation interfaces, one-product factories, pass-through wrappers, unused extension points, generic frameworks for one case, duplicate helpers or vocabulary, native capabilities replaced by dependencies, impossible-state branches better expressed as invariants, and broad refactors bundled with narrow fixes.

Also flag hidden side effects or control flow; excessive callbacks, wrappers, reflection, metaprogramming, or dynamic dispatch; nesting deeper than two levels; dense expressions that hide intermediate state; and comments or tests that merely restate implementation. Each function, class, and logic block should briefly explain what and why. Docstrings should weave those ideas naturally without separate `Why:` or `Example:` headings and cover each relevant supported language when examples are present.

Do not flag necessary complexity merely because it is complex. Security boundaries, migrations, transactions, accessibility, hardware realities, and explicit requirements may justify it.

## Finding Format

Order findings by severity. Each finding should contain:

- **Severity and title**
- **Location** — file and line
- **Impact** — concrete failure, maintenance cost, or comprehension problem
- **Evidence** — relevant execution path or code behavior
- **Smallest fix** — direct correction without redesigning unrelated code

If no actionable issue exists, say so and briefly mention residual validation gaps. Do not invent findings. Before finishing, confirm the root cause is fixed at the correct owner; required validation, authorization, error handling, and accessibility remain; names and operational strings are searchable; tests prove behavior; and deferred limits are explicit when material.
