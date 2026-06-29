# Distributed Systems Glossary

Objective: define the first distributed-systems vocabulary I need for AI infrastructure: distributed system, partial failure, availability, fault tolerance, replication, consistency, scalability, throughput, latency, and tail latency.

## Sources

- MIT 6.5840 home page: https://pdos.csail.mit.edu/6.824/
- MIT 6.5840 Lecture 1 notes: https://pdos.csail.mit.edu/6.824/notes/l01.txt
- Google Research, "The Tail at Scale": https://research.google.com/pubs/pub40801.html

## Reading Notes

### 2026-06-29 - Finished MIT 6.5840 Lecture 1 skim

Main observation: the MIT reading uses systems like MapReduce as concrete examples of distributed computation. For Day 2, treat MapReduce as an example of the broader distributed-systems vocabulary. The deeper MapReduce paper/lecture is Day 3.

MIT 6.5840 says distributed systems are hard because:

- concurrency: many computers execute at the same time, so behavior depends on timing and interleavings.
- complex interactions: components communicate over networks, and the combined system behavior is harder to reason about than one local program.
- performance bottlenecks: communication, coordination, and shared resources can limit the speedup from adding machines.
- partial failure: one machine, disk, network link, or process can fail while the rest of the system keeps running.

MIT 6.5840 says distributed systems are useful because:

- capacity through parallel processing: many machines can divide work, as in a MapReduce-style computation.
- fault tolerance through replication: multiple servers can store or serve the same state so one failure does not necessarily stop the service.
- physical distribution: systems can place computation or storage near users, devices, or data.
- isolation/security: distributed components can be separated across machines, services, or trust boundaries.

MapReduce connection for Day 3:

- Map phase: split work across many workers.
- Reduce phase: combine intermediate results into final outputs.
- Systems lesson: the framework has to schedule tasks, move data, handle stragglers, retry failures, and hide distributed complexity from user code.

Google Research "The Tail at Scale" says tail latency matters because:

- high-percentile latency:
- scale:
- utilization:
- tail-tolerant design:

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

## AI Infrastructure Mapping

| Distributed-systems concept | Training example | Inference/SGLang example | Cluster/platform example |
| --- | --- | --- | --- |
| Partial failure |  |  |  |
| Availability |  |  |  |
| Consistency |  |  |  |
| Scalability |  |  |  |
| Tail latency |  |  |  |

## Open Questions

- 
