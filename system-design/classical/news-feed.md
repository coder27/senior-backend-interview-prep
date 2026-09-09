# Design a News Feed

*Classical Distributed Systems · Focus: Data modeling, scalability · ~75 min*

## The practice prompt

Design a social news feed.

## What a strong answer covers

- Fan-out-on-write vs. fan-out-on-read, and the celebrity-account problem that breaks pure fan-out-on-write
- Feed storage model and how ranking gets computed without recomputing from scratch on every request
- How much staleness the feed can tolerate vs. where you need strict consistency

## Rubric

See [the shared rubric](../rubric.md).

## Likely follow-up

<details>
<summary>Design first, then reveal</summary>

One account has 50 million followers and posts several times a day. Does your fan-out strategy still hold, and if not, what breaks first?
</details>
