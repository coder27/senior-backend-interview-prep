# Design a URL Shortener

*Classical Distributed Systems · Focus: Scalability, data modeling · ~75 min*

## The practice prompt

Design a service like bit.ly: given a long URL, generate a short one that redirects to it.

## What a strong answer covers

- ID generation approach (counter + base62 vs. hash) and how you'd handle collisions
- The read/write ratio (reads vastly outnumber writes) and what that implies for caching
- Adding custom slugs and per-link analytics without slowing down the redirect path
- What the redirect service does when its backing store is briefly unavailable

## Rubric

See [the shared rubric](../rubric.md).

## Likely follow-up

<details>
<summary>Design first, then reveal</summary>

Now a marketing team wants custom, human-readable slugs and click analytics per link, without slowing down redirects. How does your design change?
</details>
