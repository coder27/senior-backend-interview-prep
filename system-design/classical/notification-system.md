# Design a Notification System

*Classical Distributed Systems · Focus: Scalability, reliability · ~75 min*

## The practice prompt

Design a system that sends notifications (email, SMS, push) triggered by events across a product.

## What a strong answer covers

- Why a queue sits between the trigger and delivery, and the fan-out architecture that follows
- Per-channel retry/backoff and dead-lettering for permanent failures
- Per-user rate limiting so one noisy feature can't spam a user across every channel at once
- How you'd detect a silent delivery failure — a provider that accepts the message but never delivers it

## Rubric

See [the shared rubric](../rubric.md).

## Likely follow-up

<details>
<summary>Design first, then reveal</summary>

The SMS provider starts silently dropping 5% of messages with no error response. How would you even detect that, and what's your mitigation?
</details>
