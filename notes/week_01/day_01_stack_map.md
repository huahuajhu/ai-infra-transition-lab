# Week 1 Day 1 - AI Infrastructure Stack

Objective: explain why AI infrastructure is a systems field, not only an ML modeling field.

## Progress Log

### 2026-06-28 - Finished "First Steps: Training on One GPU"

Source: Hugging Face Ultra-Scale Playbook, "First Steps: Training on One GPU"

Current learning theme:

Large-model training is a memory-management problem. We trade compute, time, and implementation complexity to fit bigger batches, longer sequences, and larger models onto limited GPU memory.

Questions and clarifications captured so far:

1. Where is batch size in the training diagram?

   Batch size is not drawn explicitly. It is hidden inside the forward/backward arrows as the number of examples processed together.

2. What is activation recomputation?

   Save only checkpoint activations, discard intermediate activations, and rerun parts of the forward pass during backward so gradients can still be computed.

3. What is full vs selective activation recomputation?

   Full recomputation reruns whole chunks or blocks. Selective recomputation keeps some activations and recomputes only the parts that are expensive in memory.

4. What is the point of full recomputation if we discard everything?

   We do not discard everything. We keep boundary checkpoints, such as the input to a block, and recreate internal activations later.

5. What is gradient accumulation?

   Split a large batch into smaller micro-batches, run forward/backward repeatedly, accumulate gradients, then do one optimizer step.

Mental model:

```text
batch size -> activation memory
activation recomputation -> saves activation memory by spending extra compute
gradient accumulation -> simulates large batch size without fitting it all in memory at once
```

## CS336 Field Map

| CS336 item | What it is really about | AI infra layer | Why I should care |
| --- | --- | --- | --- |
| Assignment 2: Systems | Profile/benchmark model layers, implement FlashAttention2 in Triton, build memory-efficient distributed training | Kernel/performance + training runtime | This is the bridge from "I can train a model" to "I can make training efficient." |
| Lecture 5: GPUs | GPU architecture and performance model | Hardware/network + kernel/performance | GPU memory hierarchy and utilization explain why training is expensive. |
| Lecture 6: Kernels, Triton | Custom GPU kernels | Kernel/performance | Kernels are where high-level model math becomes hardware-efficient code. |
| Lectures 7-8: Parallelism | Split training across devices | Training runtime + communication | Parallelism is how models exceed one GPU, but it introduces communication cost. |
| Lecture 10: Inference | Serving trained models | Inference runtime | Inference has different bottlenecks: KV cache, batching, latency, throughput. |
| Lectures 15-17: Alignment/RL | SFT/RLHF/RL post-training | Post-training infrastructure | Post-training needs rollout workers, rewards, sandboxes, queues, and observability. |
| Assignment 4: Data | Convert raw web data into usable pretraining data | Data pipeline | Model quality and training throughput depend on data pipeline quality. |

## AI Infrastructure Stack Map

| Layer | What it owns | Typical bottleneck | Example tools/projects | What I already know | What I need to learn |
| --- | --- | --- | --- | --- | --- |
| Data pipeline | Pretraining/finetuning data movement, filtering, dedupe, batching | Storage throughput, data quality, pipeline stalls | Spark, Ray, object storage, dataset loaders | Production data/ML pipeline experience, feature engineering, data validation, Hadoop/Teradata background, AWS/Kinesis/Flink streaming, and ML dataset preparation | LLM-scale pretraining data pipelines: Common Crawl processing, deduplication, filtering, tokenization throughput, packed sequences, dataset sharding, and data quality evaluation |
| Training runtime | Forward/backward/optimizer loop, distributed execution | GPU memory, communication, checkpointing | PyTorch DDP/FSDP, TorchTitan, DeepSpeed, Megatron | PyTorch/Kubeflow workflow experience; now building intuition for batch size, activation memory, activation recomputation, and gradient accumulation | FSDP/ZeRO memory sharding, distributed checkpointing, communication overlap, and failure recovery |
| Inference runtime | Request batching, KV cache, decoding, serving latency | KV memory, TTFT, throughput, tail latency | vLLM, SGLang, TensorRT-LLM | Production LLM/RAG and agent services, FastAPI/Flask APIs, two-stage retrieval/ranking, model evaluation pipelines, MCP/service tooling, and observability for AI services | vLLM/SGLang internals, continuous batching, KV cache layout, prefix caching, TTFT/ITL/goodput metrics, serving correctness, and load-testing LLM serving systems |
| Cluster scheduler | Placement, quotas, preemption, gang scheduling | Fragmentation, fairness, low utilization | Kubernetes, Kueue, Volcano, Slurm, Ray | Kubernetes, Kubeflow Pipelines, Docker, Helm, ArgoCD, AWS infrastructure, CI/CD, platform onboarding, and production service operations | GPU/TPU-specific scheduling, Kueue/Volcano/Slurm/Ray resource models, gang scheduling, topology-aware placement, fair-share quota, preemption policy, and utilization/capacity modeling |
| Observability/reliability | Metrics, traces, logs, incident response, recovery | Missing signals, high-cardinality metrics, slow recovery | OpenTelemetry, Prometheus, Datadog, runbooks | OpenTelemetry, Datadog, structured logging, production service monitoring, platform runbooks, and multi-service AI system operations | Training-specific observability: GPU/NCCL/node metrics, tokens/sec and step-time metrics, high-cardinality control, distributed trace design for jobs, failure injection, and recovery SLOs |
| Kernel/performance | Low-level compute efficiency | Memory bandwidth, occupancy, launch overhead | CUDA, Triton, PyTorch profiler, Nsight | High-level PyTorch/TensorFlow model work and initial understanding that memory hierarchy and kernel efficiency drive training cost | CUDA/Triton programming, GPU memory hierarchy, occupancy, coalescing, fused kernels, FlashAttention, PyTorch profiler, Nsight Systems, and benchmark methodology |
| Compiler/runtime | Graph lowering, fusion, sharding, hardware mapping | Bad fusion, compile time, inefficient HLO/IR | XLA, MLIR, StableHLO, Pallas | High-level ML framework usage and some awareness that frameworks lower model code into accelerator execution graphs | JAX/XLA/Pallas, HLO/StableHLO, MLIR basics, operator fusion, SPMD partitioning, sharding strategies, and how compiler decisions affect runtime performance |
| Hardware/network | GPUs/TPUs, host memory, NICs, interconnect | Bandwidth, topology, failures, thermal/power limits | H100, TPU, NVLink, InfiniBand, NCCL | Cloud-native ML infrastructure, Kubernetes production environments, GPU experiment awareness, Linux fundamentals, and AWS platform operations | GPU/TPU architecture, HBM vs host memory, PCIe/NVLink/InfiniBand/RDMA, NCCL topology, bandwidth/latency debugging, node health, and hardware-aware scheduling |

## Bottleneck Table

| Bottleneck | What causes it | Symptom | First debugging question |
| --- | --- | --- | --- |
| Memory | Model weights, gradients, optimizer states, and activations; activation memory grows with batch size and sequence length | CUDA OOM, tiny usable batch size, need for recomputation or gradient accumulation | Which tensor category is dominating peak memory, and at which phase: forward, backward, or optimizer step? |
| Compute efficiency | Underutilized GPU due to small batches, slow kernels, unfused operations, CPU/data-loader stalls, inefficient tensor shapes, or too much Python overhead | Low GPU utilization, low tokens/sec, high step time, profiler shows gaps or slow kernels | Is the accelerator busy, or is it waiting on CPU, data loading, kernel launch overhead, memory bandwidth, or communication? |
| Communication | All-reduce, all-gather, reduce-scatter, pipeline sends/receives, parameter sharding, poor topology placement, or network congestion | Scaling efficiency drops when adding GPUs, step time grows, NCCL time dominates, GPUs idle while waiting for collectives | Which collective is on the critical path, how much data moves, and are ranks placed on a good topology? |
| Scheduling/resource allocation | Fragmented GPUs, partial placement of distributed jobs, quota conflicts, missing gang scheduling, preemption without checkpoint awareness, or mixed training/inference workloads | Jobs pending despite free GPUs, low cluster utilization, unfair queueing, failed distributed launches, wasted work after preemption | Is the job waiting because of quota, device type, topology, gang requirements, priority, or lack of contiguous resources? |
| Reliability/fault recovery | Worker/node failure, OOM, flaky storage, checkpoint corruption, retry storms, bad rollout sandbox behavior, or missing health signals | Long-running jobs restart from scratch, lost work, repeated failures, silent metric gaps, slow incident diagnosis | What failed, what state was durable, how much work was lost, and can the job resume safely from the last checkpoint? |

## Checkpoint Questions

Status: source-grounded questions 1-5 completed with high confidence. See `checkpoints/week_01_day_01.md`.

### A. Source-grounded questions from "First Steps: Training on One GPU"

1. Where is batch size represented in the forward/backward training picture?

   Batch size is not drawn explicitly. It is hidden inside the forward/backward arrows as the number of examples processed together.

2. What is activation recomputation, in plain English?

   Save only checkpoint activations, discard intermediate activations, and rerun parts of the forward pass during backward so gradients can still be computed.

3. What is the difference between full and selective activation recomputation?

   Full recomputation reruns whole chunks or blocks. Selective recomputation keeps some activations and recomputes only the parts that are expensive in memory.

4. If full recomputation discards intermediate activations, what does it still keep?

   It keeps boundary checkpoints, such as the input to a block, and recreates internal activations later.

5. What is gradient accumulation, and why does it help when a large batch does not fit in memory?

   Split a large batch into smaller micro-batches, run forward/backward repeatedly, accumulate gradients, then do one optimizer step.

### B. Synthesis questions from the stack map

These are not answered by "First Steps: Training on One GPU" alone. They are first-pass synthesis questions from the CS336 field map and the stack map. It is fine to revise them later.

6. What is the difference between a training runtime and a cluster scheduler?

7. What is the difference between an inference runtime and a model API?

8. Why does communication overhead keep accelerators idle?

9. Which layer of the stack would own checkpoint/restart after a worker failure?

10. Which two stack layers are closest to your current experience?
