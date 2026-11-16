# VIP Escalation Definition

This document defines how the platform escalates unresolved VIP tickets now.

## Scope

- Defines the escalation workflow for unresolved VIP tickets.

## Inherits From

- [Ticket routing definition](ticket-routing-definition.md)

## Governing Principles

- [Support operations principles](support-operations-principles.md): separate notification from state mutation, and escalate by threshold.

## Behavior

A ticket is eligible when it belongs to a VIP or enterprise account and has not reached a terminal state.

- When an eligible ticket is unassigned for more than 10 minutes, the system pages the on-duty support lead.
- When an eligible ticket is unresolved for more than 60 minutes, the system raises an escalation event for leadership review.
- Escalation sends notifications only. It does not change ticket priority, status, or assignment.
- Thresholds are measured from the most recent reopen or creation time, whichever is later.
- A manually paused ticket does not escalate while the pause is active.

Mechanism: escalation workers scan eligible tickets every minute. Each worker suppresses a repeat notification for a threshold crossing it has already sent, using an in-memory record of sent crossings. The record is not shared between workers and is not persisted; it is empty after a worker restarts.

## Verification

- `make check` runs unit tests for threshold crossing, pause suppression, single-worker duplicate suppression, and the reopen timing reset.
