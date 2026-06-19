# ADR-002: Dispatcher Pattern

## Status

Accepted

---

## Context

Vertical Slice architectures require a mechanism to dispatch commands and queries to their respective handlers.

The selected approach should:

* Support Vertical Slice Architecture
* Avoid unnecessary dependencies
* Remain understandable by developers and AI systems
* Support future pipeline behaviors
* Avoid commercial licensing restrictions

---

## Decision

Projects shall implement an internal dispatcher abstraction.

Preferred interfaces:

ICommand<TResponse>

IQuery<TResponse>

ICommandHandler<TCommand, TResponse>

IQueryHandler<TQuery, TResponse>

IDispatcher

---

## Rationale

Benefits:

* No external dependency
* Full control over implementation
* Easier debugging
* Easier AI-assisted development
* Pipeline behaviors can be introduced later

Examples:

Validation

Logging

Authorization

Transactions

Caching

---

## Alternatives Considered

### MediatR

Advantages

Mature ecosystem

Widely used

Disadvantages

External dependency

Reduced control over pipeline behavior

Decision

Rejected

---

### Direct Service Injection

Advantages

Simple

No abstraction

Disadvantages

Tighter coupling

Reduced consistency

Decision

Rejected

---

## Consequences

Projects should implement a lightweight dispatcher.

Pipeline behaviors remain optional.
