# Design Search Autocomplete

*Classical Distributed Systems · Focus: Caching, scalability · ~75 min*

## The practice prompt

Design a typeahead/autocomplete system for a search box.

## What a strong answer covers

- Data structure trade-off: a trie for prefix matching vs. precomputed top-k suggestion lists
- Freshness requirement — how new/trending terms get in without a full rebuild
- The latency budget (usually sub-100ms) and what that rules out architecturally
- Global suggestions vs. personalized ones, and what personalization actually costs

## Rubric

See [the shared rubric](../rubric.md).

## Likely follow-up

<details>
<summary>Design first, then reveal</summary>

Trending searches need to show up in suggestions within minutes, not the next daily batch job. What has to change?
</details>
