# Design a Leaderboard/Ranking System

*Classical Distributed Systems · Focus: Data modeling, consistency trade-offs · ~75 min*

## The practice prompt

Design a real-time leaderboard for a game or platform with millions of users.

## What a strong answer covers

- A data structure for fast rank lookups at scale (sorted sets / skip lists), not a naive sort on every read
- Consistent, defined tie-handling
- Whether every score update needs to be reflected instantly, or a small lag is acceptable
- Scoped views ("rank among my friends") without maintaining a full separate leaderboard per scope

## Rubric

See [the shared rubric](../rubric.md).

## Likely follow-up

<details>
<summary>Design first, then reveal</summary>

Someone asks for "my rank among just my friends," computed live, not the global leaderboard. Does your data structure still work?
</details>
