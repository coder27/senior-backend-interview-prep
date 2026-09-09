# Design a Rate Limiter

*Classical Distributed Systems · Focus: API design, scalability · ~75 min*

## The practice prompt

Design a rate limiter for a public API.

## What a strong answer covers

- Algorithm trade-off: token bucket allows bursts, sliding window is smoother, fixed window is simplest but bursty at boundaries
- Where enforcement actually lives (gateway vs. per-service) and why that matters once you're distributed
- Per-user vs. per-IP vs. per-API-key limits, and what each is actually protecting against
- What happens when the limiter's own datastore is unavailable — fail open or fail closed, and why

## Rubric

See [the shared rubric](../rubric.md).

## Likely follow-up

<details>
<summary>Design first, then reveal</summary>

One customer is on a burst-heavy usage pattern that keeps tripping the limiter and generating support tickets. What would you change, and what does it cost you?
</details>
