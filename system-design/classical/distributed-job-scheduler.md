# Design a Distributed Job Scheduler

*Classical Distributed Systems · Focus: Reliability, consistency trade-offs · ~75 min*

## The practice prompt

Design a system that schedules and reliably executes jobs (cron-like and one-off) across a fleet of workers.

## What a strong answer covers

- At-least-once vs. exactly-once execution, and why exactly-once is expensive and often unnecessary
- Leader election or locking to stop two workers from claiming the same job
- Handling a worker crash mid-job — idempotent retries or checkpointing, not retry-from-scratch
- Clock skew's effect on cron-style scheduling across a fleet of machines

## Rubric

See [the shared rubric](../rubric.md).

## Likely follow-up

<details>
<summary>Design first, then reveal</summary>

Two workers just picked up the same job at the same time because of a scheduling race. How does your design prevent or recover from that?
</details>
