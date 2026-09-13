# Design a URL Shortener

**Round:** HLD · **Difficulty:** Easy · **Date:** 2026-09-13 · **Duration:** 5m 33s

## Problem

Design a URL shortening service like TinyURL or Bit.ly. Users submit a long URL and receive a short URL; visiting the short URL redirects to the original. Walk me through the requirements, the API, the data model, how you generate short codes, and how you would scale reads.

## Session artifacts

- [Transcript](./transcript.md)

## Evaluation

**Overall:** 2/5

The candidate demonstrated a basic understanding of the problem and proposed a valid approach using a single key-value store. However, they did not provide a clear scope, discuss non-functional requirements, or address the concerns raised about the design. The candidate also did not provide any diagrams or code that reflected a design. The design remained static and did not evolve with feedback. The candidate's responses were not detailed or well-justified, and they did not provide any trade-off reasoning for their choices. Overall, the candidate's answer was weak and did not meet the expectations of a senior engineer at a top tech company.

### Scores

| Dimension | Score | Notes |
| --- | --- | --- |
| Requirements & Scope | 2/5 | The candidate started by discussing the scale of users but did not provide a clear estimate or scope for the system. They also did not mention any non-functional requirements or constraints. |
| High-Level Architecture | 2/5 | The candidate proposed a single key-value store to handle both short and long URLs, which is a valid approach. However, they did not discuss the API, data flow, or the high-level components of the system. |
| Scalability & Bottlenecks | 2/5 | The candidate mentioned using a key-value store and a caching layer, which are good choices for scalability. However, they did not discuss how to handle high read-to-write ratios or the specific bottlenecks that might arise in the system. |
| Reliability & Resilience | 2/5 | The candidate briefly mentioned the need for a separate database to handle duplicates but did not discuss replication, failover, or other resilience measures. They also did not mention consistency vs. availability trade-offs. |
| Trade-off Reasoning | 2/5 | The candidate did not provide any trade-off reasoning for their choices. They simply stated that a single key-value store would suffice and did not justify why this was the best approach. |
| Diagram Quality | 1/5 | The candidate did not provide any diagram or visual representation of the architecture. The final code provided is a simple print statement and does not reflect any design or architecture. |
| Design Trajectory | 1/5 | The candidate did not respond to the interviewer's concerns or iterate on the design. They did not address the concerns raised about the separate database for duplicates or the need for a caching layer. The design remained static and did not evolve with feedback. |
| Communication | 2/5 | The candidate provided a basic understanding of the problem and attempted to address the interviewer's questions. However, their responses were not detailed or well-justified. They also did not provide any diagrams or code that reflected a design. |

### Strengths

- Understood the core functionality of the URL shortener service.
- Proposed using a single key-value store to handle both short and long URLs.

### Areas to improve

- Did not provide a clear estimate or scope for the system.
- Did not mention any non-functional requirements or constraints.
- Did not discuss the API, data flow, or the high-level components of the system.
- Did not address the concerns raised about the separate database for duplicates or the need for a caching layer.
- Did not provide any trade-off reasoning for their choices.
- Did not provide any diagrams or code that reflected a design.

### What a model answer covers

- Clearly defined functional and non-functional requirements.
- Discussed the API, data flow, and high-level components of the system.
- Addressed concerns raised about the separate database for duplicates and the need for a caching layer.
- Provided trade-off reasoning for their choices.
- Provided diagrams or code that reflected a design.
