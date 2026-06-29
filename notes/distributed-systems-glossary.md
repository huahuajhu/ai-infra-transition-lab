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

- high-percentile latency: p95, p99, and p99.9 latency can matter more than average latency for user-visible responsiveness.
- scale: when one request touches many machines, the chance that at least one component is slow increases.
- utilization: pushing systems closer to full utilization can make the slowest requests much slower.
- tail-tolerant design: the system needs techniques that make the whole service predictably responsive even when individual components vary.

## Glossary

| Term | Source-grounded definition | AI infrastructure example | Confidence |
| --- | --- | --- | --- |
| Distributed system | A system made of multiple networked computers that cooperate to provide storage, communication, or computation. | A distributed training job uses many GPU workers but should behave like one coordinated training run. | High |
| Partial failure | A failure mode where one component fails while other components keep running. This is harder than a single-machine crash because the rest of the system must detect, isolate, or recover from the failed part. | One training worker, GPU, node, or network link fails while the other ranks are still alive. | High |
| Availability | A service is available when it continues to respond to clients even when some failures occur. | An LLM inference endpoint keeps serving requests while one replica is restarted or one node is drained. | High |
| Fault tolerance | Fault tolerance means the system can continue operating despite component failures. | A long-running training job resumes from checkpoint instead of restarting from step zero after a worker failure. | High |
| Replication | Replication keeps multiple copies of data or service state so the system can survive a failed server and spread work across machines. | Model-serving replicas run behind a load balancer; checkpoint metadata may be stored redundantly so recovery does not depend on one machine. | High |
| Consistency | Consistency means replicated data or distributed state follows a well-defined behavior so clients or workers do not see conflicting results. | After restart, all training ranks must agree on the same checkpoint step, optimizer state, and data position. | High |
| Scalability | Scalability means performance can improve as more machines are added, especially by increasing total throughput through parallel work. | Adding more GPUs should increase useful tokens/sec or requests/sec, not just increase allocated hardware. | High |
| Throughput | Throughput is the amount of work completed per unit time; MIT frames scalable performance as many computers doing many tasks in parallel. | Training throughput can be measured as tokens/sec; serving throughput can be measured as completed requests/sec or generated tokens/sec. | High |
| Latency | Latency is the time one operation takes from request/start to response/finish. MIT Lecture 1 focuses more on scalable throughput than a formal latency definition, so this row should be refined during serving work. | For SGLang serving, latency includes time-to-first-token and inter-token latency for one request. | Medium |
| Tail latency | Tail latency is high-percentile latency such as p95, p99, or p99.9; at scale, rare slow components can dominate overall user-visible latency. | Even if average time-to-first-token is good, p99 TTFT can make an LLM product feel unreliable. | High |

## AI Infrastructure Mapping

| Distributed-systems concept | Training example | Inference/SGLang example | Cluster/platform example |
| --- | --- | --- | --- |
| Partial failure | One GPU worker dies while the rest of the distributed job is still alive. | One serving replica crashes while other replicas keep accepting requests. | One node, device plugin, or network path fails without the whole cluster going down. |
| Availability | Training can resume from checkpoint after a failure instead of losing the whole run. | SGLang service keeps responding while a replica restarts or traffic shifts. | Scheduler and API server remain usable during node maintenance or worker failures. |
| Consistency | All ranks reload the same checkpoint step, optimizer state, and RNG/data position. | Clients should not see contradictory state when requests are routed across replicas or cache state changes. | Scheduler state should not admit the same GPU to two jobs or lose quota/accounting state. |
| Scalability | More GPUs increase useful tokens/sec without communication erasing the benefit. | More serving replicas increase goodput while keeping TTFT and ITL within target. | More nodes increase schedulable capacity without excessive queueing or fragmentation. |
| Tail latency | One slow rank can make the whole training step wait, creating a step-time tail. | p99 time-to-first-token or inter-token latency is bad even when average latency looks fine. | p99 scheduling delay matters because users experience the slowest job admissions, not the average. |

## Open Questions

- MIT Lecture 1 focuses more on throughput and scalable performance than formal latency definitions. Revisit latency during Week 5 SGLang serving.
