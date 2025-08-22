# Architectural Decision Records (ADRs)

This folder contains important architectural decisions made during the development of Rush2.ai. These documents explain not just what we decided, but **why** we made these choices.

## Purpose

- Record significant architectural decisions
- Explain the context and rationale
- Document trade-offs and alternatives considered
- Provide future developers (including ourselves) with historical context

## Index of Decisions

| ADR | Title | Status | Date |
|-----|-------|--------|------|
| [001](001-authentication-strategy.md) | Authentication Strategy - NextAuth Now, Ory Kratos Later | Accepted | 2025-08-22 |

## Format

Each ADR follows this structure:
- **Context**: What prompted this decision?
- **Decision**: What did we decide?
- **Rationale**: Why did we make this choice?
- **Consequences**: What are the trade-offs?
- **Implementation**: How will we execute this?

## When to Create an ADR

Create a new ADR when:
- Choosing between multiple technical approaches
- Making decisions that will be hard to reverse
- Selecting key technologies or frameworks
- Defining system boundaries or interfaces
- Making security or compliance decisions

## Memory System Integration

These decisions should be stored in mem0 when available for quick context retrieval. Until then, they serve as our source of truth for architectural choices.

## Related Documentation

- [Task Master Tasks](/.taskmaster/tasks/)
- [PRD](../PRD/rush2ai.prd)
- [Setup Guides](../../*.md)