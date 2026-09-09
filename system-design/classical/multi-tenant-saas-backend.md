# Design a Multi-Tenant SaaS Backend

*Classical Distributed Systems · Focus: Data modeling, reliability · ~75 min*

## The practice prompt

Design the data layer for a B2B SaaS product serving many customers (tenants).

## What a strong answer covers

- Isolation strategy (shared schema with tenant_id vs. schema-per-tenant vs. database-per-tenant) and its operational cost
- Noisy-neighbor protection so one tenant's load can't degrade everyone else's
- Supporting one tenant's schema customization without forking the entire data model
- Tenant-level backup, restore, and data deletion for compliance

## Rubric

See [the shared rubric](../rubric.md).

## Likely follow-up

<details>
<summary>Design first, then reveal</summary>

Your single largest customer just asked for a contractual guarantee that their data never shares infrastructure with anyone else. What does that actually cost you to support?
</details>
