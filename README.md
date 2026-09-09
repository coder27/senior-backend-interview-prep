# Senior Backend Interview Prep (2026)

A focused prep set for senior (L6-equivalent) backend interviews at product companies and GCCs, built to reflect how the bar actually moved in 2026 rather than recycling pre-2024 material.

## Why this exists

Three things changed that most existing prep material hasn't caught up with:

- **Cost and operational reasoning are now graded explicitly.** "Add more servers" stopped being a sufficient answer; interviewers expect you to reason about cost trade-offs and failure modes as a first-class part of the design.
- **AI/LLM infrastructure now shows up in general backend loops**, not just ML-specialist interviews — RAG pipelines, LLM-serving gateways, and third-party-LLM integrations are mainstream senior system design questions now.
- **Interviewers deliberately shift requirements mid-interview** to see whether you can adapt, specifically to defeat memorized, ChatGPT-polished answers.

Every system design prompt here has a hidden "likely follow-up" for exactly that reason — design the system, then reveal the curveball and see if your design holds up.

## What's in here

- [`system-design.md`](system-design.md) — 19 senior-level prompts across 9 focus areas (including AI/LLM infrastructure and cost/operational reasoning), each with a rubric and a hidden follow-up curveball. **Start here** — this is the part that's actually different from what else is out there.
- [`dsa.md`](dsa.md) — 60 well-known problems organized by pattern, linking out to LeetCode for the actual solving (its judge does that better than anything homegrown).
- [`behavioral.md`](behavioral.md) — 28 questions across 7 categories, with a rubric for what a strong senior-level STAR story actually looks like.
- [`resources.md`](resources.md) — other genuinely good, actively maintained OSS prep resources worth pairing with this.

## How to use it

Pick one system design prompt. Give yourself the full time box (~75 min) to actually design it — requirements, high-level design, deep dives, trade-offs, cost. Then reveal the follow-up and think through how your design adapts. That adaptation is the actual skill being tested in 2026, not the initial design.

## License

MIT — use it, fork it, adapt it. If you find something worth adding or correcting, a PR is welcome.
