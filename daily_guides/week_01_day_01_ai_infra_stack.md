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

### 25-35 minutes - Build a CS336 field map

Do not read CS336 deeply today. Use it as an index of what serious language-model systems work includes.

- Stanford CS336: https://cs336.stanford.edu/spring2025/

Your task is to map each CS336 topic to one layer of your AI infrastructure stack. Open the page, inspect the assignments and schedule, and fill the table below in `notes/week_01/day_01_stack_map.md`.

```markdown
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
```

What you are learning from this section:

- The course is not just "LLM theory"; it is implementation-heavy systems work.
- Modern AI infrastructure spans data, training runtime, kernels, GPUs, inference, and post-training.
- Your plan is organized around the same stack, but at a 1-hour/day pace.

If you only have 5 minutes, fill the `Why I should care` column for Assignment 2, Lectures 7-8, and Lecture 10.

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
