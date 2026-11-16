# Support Operations Principles

This document states the intent for support workflow behavior: what it must achieve and why. Current behavior is in the definitions.

## Prioritize Determinism At Intake

- Intake and routing decide from explicit ticket facts and reviewable policy, not from judgment at intake time.
- This keeps priority and queue behavior testable and explainable.
- Violation condition: two tickets with the same facts, under the same policy, land in different queues.

## Separate Notification From State Mutation

- Notifications and pages do not change core ticket state. State changes happen through explicit transitions so operators can audit them.
- Violation condition: a notification or page changes a ticket's priority, status, or assignment.

## Escalate By Threshold, Not Emotion

- Escalation triggers from clear thresholds and policy rules, once per threshold crossing.
- This reduces inconsistency between operators and keeps paging predictable.
- Violation condition: an escalation fires for a ticket that has not crossed a threshold, or one threshold crossing pages the support lead more than once.
