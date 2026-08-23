# HighLevelDesign

Study notes for **System Design fundamentals**, based on _System Design Interview_ by
Alex Xu (Volume 1), Chapters 1–3. These three chapters are the core foundation: how
systems scale, how to estimate capacity, and how to run the interview itself.

## Notes Index

| # | Chapter | What it covers | Notes |
|---|---|---|---|
| 1 | Scale From Zero to Millions | How a system evolves from a single server to a multi-region, sharded, cached architecture | [notes/01-scale-from-zero-to-millions.md](notes/01-scale-from-zero-to-millions.md) |
| 2 | Back-of-the-Envelope Estimation | Powers of two, latency & availability numbers, QPS/storage estimation | [notes/02-back-of-envelope-estimation.md](notes/02-back-of-envelope-estimation.md) |
| 3 | Framework for System Design Interviews | The 4-step process to structure any design interview | [notes/03-framework-for-system-design-interviews.md](notes/03-framework-for-system-design-interviews.md) |

## Suggested Study Order

1. **Chapter 3 first (the framework)** — learn *how* to approach a problem before the
   building blocks. It's the mental scaffold you'll reuse in every question.
2. **Chapter 1 (scaling)** — the vocabulary and components (load balancer, cache, replica,
   shard, queue) you'll assemble during a design.
3. **Chapter 2 (estimation)** — the numbers that justify your design choices under scale.

Then loop back and practice: pick a system, run the **4-step framework** (Ch 3), assemble
**components** (Ch 1), and back it with **estimates** (Ch 2).

## How Each Note Is Structured

- **Detailed explanations** with mermaid architecture/flow diagrams.
- A **Cheat Sheet** section for quick revision.
- **Practice Questions** to test recall and reasoning.

## Quick Reference

- **4-step framework:** Scope → High-level design (buy-in) → Deep dive → Wrap up.
- **Scaling moves:** stateless web tier · redundancy everywhere · cache · multi–data-center
  · CDN · shard the DB · split into services · monitor + automate.
- **Estimation staples:** seconds/day ≈ 86,400 · peak QPS ≈ 2× average · KB→MB→GB→TB→PB
  (~1000× each) · memory ≈ 100 ns, disk seek ≈ 10 ms, cross-continent ≈ 150 ms.

