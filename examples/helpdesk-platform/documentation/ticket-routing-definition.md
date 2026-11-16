# Ticket Routing Definition

This document defines how the platform routes new tickets now.

## Scope

- Defines how newly created tickets are classified, prioritized, and assigned to a queue.
- Does not define the lifecycle after a ticket is assigned.

## Governing Principles

- [Support operations principles](support-operations-principles.md)

## Behavior

Every new ticket gets a priority and a queue before it becomes visible in the agent work queue. Routing reads only ticket attributes and the current policy configuration.

- Tickets from customers with an active enterprise plan enter the `enterprise-support` queue by default.
- Tickets marked as security-sensitive enter the `security-review` queue regardless of product area.
- When a ticket matches more than one queue, the queue with the highest severity wins.
- Tickets with insufficient classification data go to `general-support`.

Triggers: ticket creation from API, email, or form intake. Policy configuration updates apply to tickets created after the update; routing does not re-route existing tickets.

Inputs: normalized ticket category, customer plan tier, and severity classification. Output: a queue assignment, applied by the work management layer as a transition.

## Verification

- `make check` runs unit tests for queue precedence, plan-tier routing, the security override, and the default fallback.
