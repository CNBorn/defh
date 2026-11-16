# Architecture Overview

This document describes the boundaries of the helpdesk platform: request intake, routing, work management, and adapters. Statements under "Architectural Intent" are principles. All other statements describe the current structure.

## Architectural Intent

- Ticket ownership stays explicit.
- Routing policy stays testable and reviewable.
- Product rules stay separate from transport and vendor adapters.

## Runtime Boundaries

1. Intake Layer
- Accepts API, email, and web form submissions.
- Normalizes inbound requests into internal ticket contracts.

2. Routing Layer
- Applies priority, queue, and assignment policy.
- Decides whether escalation rules trigger.

3. Work Management Layer
- Owns ticket state transitions, SLA timers, comments, and assignments.

4. Adapter Layer
- Integrates with email delivery, CRM sync, chat notifications, and analytics.

## Ownership

- The work management layer owns ticket status and assignment. Other layers change them only by requesting a transition.
- Routing returns a recommendation. The work management layer applies it as a transition.
- Adapter payloads are derived from internal contracts. They are not a source of ticket state.

## Dependency Direction

- Intake depends on normalization contracts.
- Routing depends on ticket contracts and policy configuration.
- Adapters depend on internal contracts and external schemas. They contain no routing policy.

## Non-goals

- Vendor-specific API details
- UI component structure
- Database table inventories
