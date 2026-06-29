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

## AI Infrastructure Stack Map

| Layer | What it owns | Typical bottleneck | Example tools/projects | What I already know | What I need to learn |
| --- | --- | --- | --- | --- | --- |
| Data pipeline | Pretraining/finetuning data movement, filtering, dedupe, batching | Storage throughput, data quality, pipeline stalls | Spark, Ray, object storage, dataset loaders |  |  |
| Training runtime | Forward/backward/optimizer loop, distributed execution | GPU memory, communication, checkpointing | PyTorch DDP/FSDP, TorchTitan, DeepSpeed, Megatron | PyTorch/Kubeflow workflow experience; now building intuition for batch size, activation memory, activation recomputation, and gradient accumulation | FSDP/ZeRO memory sharding, distributed checkpointing, communication overlap, and failure recovery |
| Inference runtime | Request batching, KV cache, decoding, serving latency | KV memory, TTFT, throughput, tail latency | vLLM, SGLang, TensorRT-LLM |  |  |
| Cluster scheduler | Placement, quotas, preemption, gang scheduling | Fragmentation, fairness, low utilization | Kubernetes, Kueue, Volcano, Slurm, Ray |  |  |
| Observability/reliability | Metrics, traces, logs, incident response, recovery | Missing signals, high-cardinality metrics, slow recovery | OpenTelemetry, Prometheus, Datadog, runbooks |  |  |
| Kernel/performance | Low-level compute efficiency | Memory bandwidth, occupancy, launch overhead | CUDA, Triton, PyTorch profiler, Nsight |  |  |
| Compiler/runtime | Graph lowering, fusion, sharding, hardware mapping | Bad fusion, compile time, inefficient HLO/IR | XLA, MLIR, StableHLO, Pallas |  |  |
| Hardware/network | GPUs/TPUs, host memory, NICs, interconnect | Bandwidth, topology, failures, thermal/power limits | H100, TPU, NVLink, InfiniBand, NCCL |  |  |

## Bottleneck Table

| Bottleneck | What causes it | Symptom | First debugging question |
| --- | --- | --- | --- |
| Memory | Model weights, gradients, optimizer states, and activations; activation memory grows with batch size and sequence length | CUDA OOM, tiny usable batch size, need for recomputation or gradient accumulation | Which tensor category is dominating peak memory, and at which phase: forward, backward, or optimizer step? |
| Compute efficiency |  |  |  |
| Communication |  |  |  |
| Scheduling/resource allocation |  |  |  |
| Reliability/fault recovery |  |  |  |

## Quiz Answers

1. During training, what four major tensor categories consume memory?

   Parameters/weights, gradients, optimizer states, and activations.

2. Why can a model fit for the first forward/backward step but fail later?

   Peak memory changes across the full training step. Activations are needed during forward/backward, gradients accumulate during backward, and optimizer state can add another large memory requirement around the optimizer step.

3. Why do long sequence lengths make activation memory painful?

   Activations are stored for many tensors across layers and tokens. Larger batch size and longer sequence length increase the amount of intermediate state needed for backward.

4. What does activation recomputation trade away to save memory?

   It saves activation memory by spending extra compute and time. Instead of storing every intermediate activation, training keeps selected checkpoint activations and reruns parts of forward during backward.

5. Name the three high-level scaling challenges from the Ultra-Scale Playbook.

   Memory usage, compute efficiency, and communication overhead.

6. What is the difference between a training runtime and a cluster scheduler?

7. What is the difference between an inference runtime and a model API?

8. Why does communication overhead keep accelerators idle?

9. Which layer of the stack would own checkpoint/restart after a worker failure?

10. Which two stack layers are closest to your current experience?
