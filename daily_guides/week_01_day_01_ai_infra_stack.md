# Week 1 Day 1 - AI Infrastructure Stack

Today should teach one real idea:

Large-model systems are not hard only because the model is smart. They are hard because every training or serving workload runs into memory limits, compute efficiency limits, communication overhead, scheduling constraints, and reliability problems.

## 60-Minute Plan

### 0-5 minutes - Write the objective

Create this file:

`notes/week_01/day_01_stack_map.md`

Write:

```markdown
# Week 1 Day 1 - AI Infrastructure Stack

Objective: explain why AI infrastructure is a systems field, not only an ML modeling field.
```

### 5-25 minutes - Read the core technical material

Read this source:

- Hugging Face Ultra-Scale Playbook: https://nanotron-ultrascale-playbook.static.hf.space/

Read these sections only:

- Opening through "High-Level Overview"
- "First Steps: Training on One GPU"
- "Memory usage in transformers"
- "Memory for weights/grads/optimizer states"
- "Memory for activations"
- "Activation recomputation"

Do not try to finish the whole playbook today. Your goal is to understand the first bottleneck story:

- A training step has forward, backward, and optimizer phases.
- Training memory is not just model weights.
- Parameters, gradients, optimizer states, and activations have different memory behavior.
- Activations grow with batch size and sequence length.
- Recomputation trades more compute for lower memory.
- Scaling up introduces a three-way tradeoff between memory usage, compute efficiency, and communication overhead.

### 25-35 minutes - Skim the curriculum map

Read the Stanford CS336 page only enough to inspect the assignments and schedule:

- Stanford CS336: https://cs336.stanford.edu/spring2025/

Focus on:

- Assignment 2: Systems
- Lecture 5: GPUs
- Lecture 6: Kernels, Triton
- Lectures 7 and 8: Parallelism
- Lecture 10: Inference
- Lectures 15 to 17: Alignment and RL

This is not the main reading. Use it as a map of the field. The point is to see that serious language-model engineering includes implementation, profiling, distributed training, GPU kernels, inference, and RL/post-training.

### 35-50 minutes - Build the artifact

In `notes/week_01/day_01_stack_map.md`, add this table and fill it in:

```markdown
## AI Infrastructure Stack Map

| Layer | What it owns | Typical bottleneck | Example tools/projects | What I already know | What I need to learn |
| --- | --- | --- | --- | --- | --- |
| Data pipeline | Pretraining/finetuning data movement, filtering, dedupe, batching | Storage throughput, data quality, pipeline stalls | Spark, Ray, object storage, dataset loaders |  |  |
| Training runtime | Forward/backward/optimizer loop, distributed execution | GPU memory, communication, checkpointing | PyTorch DDP/FSDP, TorchTitan, DeepSpeed, Megatron |  |  |
| Inference runtime | Request batching, KV cache, decoding, serving latency | KV memory, TTFT, throughput, tail latency | vLLM, SGLang, TensorRT-LLM |  |  |
| Cluster scheduler | Placement, quotas, preemption, gang scheduling | Fragmentation, fairness, low utilization | Kubernetes, Kueue, Volcano, Slurm, Ray |  |  |
| Observability/reliability | Metrics, traces, logs, incident response, recovery | Missing signals, high-cardinality metrics, slow recovery | OpenTelemetry, Prometheus, Datadog, runbooks |  |  |
| Kernel/performance | Low-level compute efficiency | Memory bandwidth, occupancy, launch overhead | CUDA, Triton, PyTorch profiler, Nsight |  |  |
| Compiler/runtime | Graph lowering, fusion, sharding, hardware mapping | Bad fusion, compile time, inefficient HLO/IR | XLA, MLIR, StableHLO, Pallas |  |  |
| Hardware/network | GPUs/TPUs, host memory, NICs, interconnect | Bandwidth, topology, failures, thermal/power limits | H100, TPU, NVLink, InfiniBand, NCCL |  |  |
```

Then add this second table:

```markdown
## Bottleneck Table

| Bottleneck | What causes it | Symptom | First debugging question |
| --- | --- | --- | --- |
| Memory |  |  |  |
| Compute efficiency |  |  |  |
| Communication |  |  |  |
| Scheduling/resource allocation |  |  |  |
| Reliability/fault recovery |  |  |  |
```

### 50-60 minutes - Quiz

Answer without looking back first. Then check your answer against the source.

1. During training, what four major tensor categories consume memory?
2. Why can a model fit for the first forward/backward step but fail later?
3. Why do long sequence lengths make activation memory painful?
4. What does activation recomputation trade away to save memory?
5. Name the three high-level scaling challenges from the Ultra-Scale Playbook.
6. What is the difference between a training runtime and a cluster scheduler?
7. What is the difference between an inference runtime and a model API?
8. Why does communication overhead keep accelerators idle?
9. Which layer of the stack would own checkpoint/restart after a worker failure?
10. Which two stack layers are closest to your current experience?

## Expected Output

By the end of the hour, you should have:

- `notes/week_01/day_01_stack_map.md`
- A filled AI infrastructure stack map
- A filled bottleneck table
- Answers to the 10 quiz questions

This is a good Day 1 if you can explain this sentence in your own words:

"AI infrastructure is the work of keeping expensive accelerators usefully busy while respecting memory limits, communication costs, scheduling constraints, and failure recovery needs."
