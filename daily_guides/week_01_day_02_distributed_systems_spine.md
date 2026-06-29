# Week 1 Day 2 - Distributed Systems Spine

Today should teach one real idea:

AI infrastructure is distributed systems work because large AI services and training jobs are built from many machines that must coordinate despite failure, variable performance, network cost, and consistency tradeoffs.

## 60-Minute Plan

### 0-5 minutes - Write the objective

Open:

`notes/distributed-systems-glossary.md`

Write today's objective:

```markdown
Objective: define the first distributed-systems vocabulary I need for AI infrastructure: distributed system, partial failure, availability, fault tolerance, replication, consistency, scalability, throughput, latency, and tail latency.
```

### 5-20 minutes - Read MIT 6.5840 as the main source

Read:

- MIT 6.5840 home page: https://pdos.csail.mit.edu/6.824/
- MIT 6.5840 Lecture 1 notes: https://pdos.csail.mit.edu/6.824/notes/l01.txt

Do not read every detail deeply. Focus on these parts:

- What is a distributed system?
- Why are distributed systems hard?
- Why are they useful?
- Main topics: storage, communication, computation.
- Fault tolerance: service continues despite failures.
- Replication: using multiple servers so one failure does not stop the system.
- Consistency: well-defined behavior even when data is replicated.
- Performance/scalability: using many servers to increase total throughput.
- Tradeoff: fault tolerance, consistency, and performance can conflict because communication is slow and hard to scale.

What to write down:

```markdown
MIT 6.5840 says distributed systems are hard because:
- concurrency:
- complex interactions:
- performance bottlenecks:
- partial failure:

MIT 6.5840 says distributed systems are useful because:
- capacity through parallel processing:
- fault tolerance through replication:
- physical distribution:
- isolation/security:
```

### 20-30 minutes - Read tail latency source

Read only the Google Research page summary:

- Google Research, "The Tail at Scale": https://research.google.com/pubs/pub40801.html

Do not read the full paper today. Your goal is only to understand why average latency is not enough.

Extract these ideas:

- Tail latency means high-percentile latency, such as p95, p99, or p99.9.
- At large scale, rare slow events can dominate user-visible performance.
- Higher utilization can make latency tails worse.
- Tail-tolerant systems try to create a predictably responsive whole from less predictable parts.

AI-infra connection:

- LLM serving cares about p95/p99 time-to-first-token and inter-token latency.
- Distributed training cares about slow workers because one slow rank can hold back the step.
- Schedulers and observability systems need tail metrics, not only averages.

### 30-45 minutes - Build the glossary artifact

In `notes/distributed-systems-glossary.md`, fill this table.

Keep each definition short: one or two sentences. The most important column is "AI infrastructure example"; that is where you connect the concept to your target career.

```markdown
## Glossary

| Term | Source-grounded definition | AI infrastructure example | Confidence |
| --- | --- | --- | --- |
| Distributed system |  |  |  |
| Partial failure |  |  |  |
| Availability |  |  |  |
| Fault tolerance |  |  |  |
| Replication |  |  |  |
| Consistency |  |  |  |
| Scalability |  |  |  |
| Throughput |  |  |  |
| Latency |  |  |  |
| Tail latency |  |  |  |
```

Use only two sources today:

- MIT 6.5840 home page and Lecture 1 for distributed systems, partial failure, availability, fault tolerance, replication, consistency, scalability, throughput, and latency.
- Google Research "The Tail at Scale" for tail latency.

### 45-55 minutes - Add an AI infrastructure mapping table

Add this second table:

```markdown
## AI Infrastructure Mapping

| Distributed-systems concept | Training example | Inference/SGLang example | Cluster/platform example |
| --- | --- | --- | --- |
| Partial failure |  |  |  |
| Availability |  |  |  |
| Consistency |  |  |  |
| Scalability |  |  |  |
| Tail latency |  |  |  |
```

Good examples:

- Partial failure: one GPU worker dies while the rest of the job is still alive.
- Availability: an inference service keeps responding while one replica or node fails.
- Consistency: all ranks reload the same checkpoint step after recovery.
- Scalability: adding nodes increases useful tokens/sec, not just allocated GPU count.
- Tail latency: p99 time-to-first-token is bad even if average latency looks fine.

### 55-60 minutes - Answer checkpoint questions

Write answers in:

`checkpoints/week_01_day_02.md`

#### A. Source-grounded questions from MIT 6.5840

1. What is a distributed system?
2. Why are distributed systems hard to build?
3. Why are distributed systems useful?
4. What does high availability mean?
5. What role does replication play in fault tolerance?
6. Why can consistency and performance conflict?
7. What does scalability mean in the Lecture 1 performance discussion?

#### B. Source-grounded question from Google Research "The Tail at Scale"

8. What is tail latency, and why can it dominate performance at scale?

#### C. Synthesis questions from your glossary

9. Which Day 2 concept is most directly connected to SGLang serving?
10. Which Day 2 concept is most directly connected to long-running distributed training jobs?

## Expected Output

By the end of the hour, you should have:

- `notes/distributed-systems-glossary.md`
- `checkpoints/week_01_day_02.md`
- One short glossary table
- One AI infrastructure mapping table
- Answers to 8 source-grounded questions and 2 synthesis questions

This is a good Day 2 if you can explain this sentence in your own words:

"Distributed systems are hard because many machines must act like one service even though individual machines, networks, and requests can be slow, inconsistent, or failed."
