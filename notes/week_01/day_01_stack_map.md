# Week 1 Day 1 - AI Infrastructure Stack

Objective: explain why AI infrastructure is a systems field, not only an ML modeling field.

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

## Bottleneck Table

| Bottleneck | What causes it | Symptom | First debugging question |
| --- | --- | --- | --- |
| Memory |  |  |  |
| Compute efficiency |  |  |  |
| Communication |  |  |  |
| Scheduling/resource allocation |  |  |  |
| Reliability/fault recovery |  |  |  |

## Quiz Answers

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
