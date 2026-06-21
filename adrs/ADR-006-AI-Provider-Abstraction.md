# ADR-006: AI-Provider-Abstraction

## Status

Accepted

---

## Context

Projects may integrate AI capabilities.

Requirements differ between customers.

Examples

OpenAI

Azure OpenAI

Ollama

Future providers

---

## Decision

AI providers shall be abstracted.

Applications shall not directly depend on provider SDKs.

---

## Example Interfaces

IChatCompletionService

IEmbeddingService

IVectorStore

IToolExecutor

IPromptRepository

ITokenUsageTracker

---

## Rationale

Benefits

Provider independence

Cost optimization

Compliance flexibility

Future extensibility

Better testing

---

## Alternatives Considered

Direct OpenAI SDK Usage

Advantages

Simple

Disadvantages

Vendor lock-in

Harder testing

Reduced flexibility

Decision

Rejected

---

## Consequences

Provider implementations remain infrastructure concerns.

Business logic remains provider agnostic.

Model deployment selection and tiering: see **ADR-015**.

Public endpoint abuse controls: see **ADR-014**.
