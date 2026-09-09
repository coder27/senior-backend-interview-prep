# Design an Idempotent Payments API

*Classical Distributed Systems · Focus: API design, reliability, cost & operational reasoning · ~75 min*

## The practice prompt

Design the API and backend for processing payments where retries are expected (client timeouts, network failures).

## What a strong answer covers

- Idempotency key design, checked before any side effect occurs, not after
- An explicit state machine for a payment's lifecycle, so a retry can't skip or repeat a state
- A reconciliation process for when your state machine and the payment provider's records disagree
- Separating the API's fast synchronous response from the actual asynchronous settlement

## Rubric

See [the shared rubric](../rubric.md).

## Likely follow-up

<details>
<summary>Design first, then reveal</summary>

Finance reports a small number of double-charges last month despite idempotency keys. Where would you actually look, and how would you prevent recurrence?
</details>
