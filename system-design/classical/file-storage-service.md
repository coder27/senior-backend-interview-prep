# Design a File Storage/Sharing Service

*Classical Distributed Systems · Focus: Data modeling, scalability · ~75 min*

## The practice prompt

Design a service like Dropbox: upload, store, sync, and share files.

## What a strong answer covers

- Chunking strategy for large files and how resumable uploads work
- Deduplication via content-addressed storage, and its privacy implications
- Sync conflict resolution when two clients edit the same file offline
- Access control model for sharing — link-based vs. ACL-based, and when each is appropriate

## Rubric

See [the shared rubric](../rubric.md).

## Likely follow-up

<details>
<summary>Design first, then reveal</summary>

Two people edit the same file offline on different laptops and reconnect at the same time. Walk through exactly what each of them sees.
</details>
