# Ticket Routing Definition

This document defines how the platform routes new tickets now.

## Scope

- Defines how newly created tickets are classified, prioritized, and assigned to a queue.
- Does not define the lifecycle after a ticket is assigned.

## Governing Principles

- [Support operations principles](support-operations-principles.md)

## Behavior

Every new ticket gets a priority and a queue before it becomes visible in the agent work queue. Routing reads only ticket attributes and the current policy configuration.

- Priority equals the ticket's severity classification: `critical`, `high`, `normal`, or `low`.
- Tickets from customers with an active enterprise plan enter the `enterprise-support` queue by default.
- Tickets marked as security-sensitive enter the `security-review` queue regardless of product area.
- When a ticket matches more than one queue, the highest-ranked queue wins. Queue rank, highest first: `security-review`, `enterprise-support`, `general-support`.
- A ticket with no category or no severity classification goes to `general-support` with priority `normal`.

Triggers: ticket creation from API, email, or form intake. Policy configuration updates apply to tickets created after the update; routing does not re-route existing tickets.

Inputs: normalized ticket category, customer plan tier, and severity classification. Output: a queue assignment, applied by the work management layer as a transition.

## Verification

- `make check` runs unit tests for priority assignment, queue rank, plan-tier routing, the security override, and the default fallback.
