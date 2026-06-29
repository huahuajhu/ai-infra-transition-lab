# Week 1 Day 2 Checkpoint

## Status

Completed first-pass glossary, AI infrastructure mapping, and checkpoint answers.

## Sources

- MIT 6.5840 home page: https://pdos.csail.mit.edu/6.824/
- MIT 6.5840 Lecture 1 notes: https://pdos.csail.mit.edu/6.824/notes/l01.txt
- Google Research, "The Tail at Scale": https://research.google.com/pubs/pub40801.html

## Type

Source-grounded + synthesis

## A. Source-Grounded Questions From MIT 6.5840

### 1. What is a distributed system?

My answer:

A distributed system is a system made of multiple networked computers that cooperate to provide storage, communication, or computation. The point is that many machines work together so users or applications can treat them as one larger service.

Confidence: High

### 2. Why are distributed systems hard to build?

My answer:

They are hard because of concurrency, complex interactions, performance bottlenecks, and partial failure. The tricky part is that one component can fail or slow down while the rest of the system keeps running, so the system must detect and handle mixed states.

Confidence: High

### 3. Why are distributed systems useful?

My answer:

They are useful because they can increase capacity through parallel processing, improve fault tolerance through replication, support physical distribution, and provide isolation or security boundaries. MapReduce is an example of using many machines to divide a large computation.

Confidence: High

### 4. What does high availability mean?

My answer:

High availability means the service continues responding to clients even when failures happen. In AI infrastructure, this could mean an inference service stays online while one replica or node fails.

Confidence: High

### 5. What role does replication play in fault tolerance?

My answer:

Replication keeps multiple copies of data or service state so one failed server does not necessarily stop the system. It helps fault tolerance because another replica can continue serving or recover the needed state.

Confidence: High

### 6. Why can consistency and performance conflict?

My answer:

Consistency and performance can conflict because keeping replicas in a well-defined state requires communication and coordination. That coordination can slow the system down, especially as the number of machines grows.

Confidence: High

### 7. What does scalability mean in the Lecture 1 performance discussion?

My answer:

Scalability means adding computers can increase useful performance, especially total throughput through parallel work. The important test is whether more machines complete more useful work, not merely whether more machines are allocated.

Confidence: High

## B. Source-Grounded Question From Google Research "The Tail at Scale"

### 8. What is tail latency, and why can it dominate performance at scale?

My answer:

Tail latency is high-percentile latency such as p95, p99, or p99.9. It can dominate performance at scale because a user request may depend on many components, and the chance that at least one component is unusually slow grows as the system fans out.

Confidence: High

## C. Synthesis Questions From The Glossary

### 9. Which Day 2 concept is most directly connected to SGLang serving?

My answer:

Tail latency is most directly connected to SGLang serving. For LLM serving, p99 time-to-first-token and inter-token latency can make the product feel slow even when average latency looks fine. Availability and scalability are also important, but tail latency is the concept that most directly maps to user-visible serving quality.

Confidence: Medium

### 10. Which Day 2 concept is most directly connected to long-running distributed training jobs?

My answer:

Partial failure is most directly connected to long-running distributed training jobs. A training run can involve many workers over many hours or days, so one failed worker, GPU, node, or network link should not force the whole run to restart from zero. Fault tolerance and consistency come next because recovery depends on valid checkpoints and all ranks agreeing on state.

Confidence: Medium

## Follow-Up

- Revisit these definitions after Week 3 observability, Week 4 distributed training, and Week 5 SGLang serving.
