# Design Playbook

Apply [communication.md](communication.md) to the design recommendation, flow, trade-offs, and deferred work.

Design the least complex system that satisfies known requirements and preserves stated invariants.

## Process

1. Restate the present problem, users, constraints, and acceptance criteria. Separate required behavior from guesses about future needs.
2. Inspect the current system. Reuse its vocabulary, boundaries, data flow, and proven patterns unless they caused the problem.
3. Start with the simplest end-to-end design. Add a component only when a current requirement forces it.
4. Keep one source of truth and a clear owner for each state transition. Preserve direct, observable data flow and useful points for logs and debugging.
5. Test failure, concurrency, security, migration, operations, and human debugging. Add complexity only for a demonstrated gap.
6. Record deferred capabilities and the concrete trigger for adding them.

## Agent-Friendly Naming

- Reuse the system's domain vocabulary so entities and concepts each have one spelling.
- Name components, boundaries, artifacts, data stores, APIs, and states after the concepts an agent will search for.
- Give generic roles domain context: prefer `invoice-validation-service` to `validation-service` and avoid bare names such as `manager`, `handler`, or `processor`.
- Make ownership and data flow apparent from names. A design should lead from a searched concept to one clear owner.
- Keep names concise but uniquely searchable; do not abbreviate away domain meaning or design concepts for hypothetical reuse.

## Reject by Default

- One-implementation interfaces, one-product factories, plugin systems without plugins, and configuration for values that do not vary
- Generic frameworks for one use case or layers that only forward arguments
- New services, queues, caches, or databases without measured need
- Hidden dispatch, metaprogramming, generated behavior, or event choreography where direct calls would work
- Designs that obscure execution order, state ownership, or failure diagnosis to reduce code size
- Performance work without a budget or measurement, and future-proofing without a named requirement

## Keep When Required

Do not remove boundaries that enforce security, ownership, transactionality, data integrity, accessibility, or recoverability. Hardware and external systems often need explicit timeouts, retries, calibration, and limits; these are requirements, not clutter.

## Design Output

1. **Decision** — one-sentence design.
2. **Flow** — short end-to-end path.
3. **Components** — only components with distinct current responsibilities.
4. **Trade-offs** — important costs or limits.
5. **Deferred** — omitted capability plus trigger for adding it.
6. **Verification** — how the design will prove correctness.

Avoid catalogs of alternatives unless the user asks. If one option clearly wins, recommend it directly.
