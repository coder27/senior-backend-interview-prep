# Design an On-Call Alerting System

*Classical Distributed Systems · Focus: Reliability, observability · ~75 min*

## The practice prompt

Design a system like PagerDuty: route alerts from monitoring systems to the right on-call engineer, with escalation if unacknowledged.

## What a strong answer covers

- Escalation policy design and what happens when nobody acknowledges an alert
- Deduping/grouping correlated noisy alerts so one root cause doesn't page five people separately
- The alerting path's own reliability — it can't depend on the systems it exists to alert about
- Correct on-call scheduling and handoff across time zones

## Rubric

See [the shared rubric](../rubric.md).

## Likely follow-up

<details>
<summary>Design first, then reveal</summary>

The alerting system itself is down during an incident — the thing meant to page people about outages is having one. How did you design around that, if at all?
</details>
