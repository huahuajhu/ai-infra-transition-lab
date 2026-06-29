# JAX Scaling Book Reading Map

Source: https://jax-ml.github.io/scaling-book/

Why this source matters:

The JAX Scaling Book is now a core source in this plan, not an optional extra. It connects the exact ideas that make AI infrastructure hard: roofline limits, GPUs/TPUs, sharding, transformer memory, training throughput, inference latency, profiling, and JAX/XLA execution.

Use it as a systems lens. You do not need to read the whole book straight through. Read the assigned chapter when it matches the weekly artifact.

## Chapter Map

| Chapter | Link | Use in this plan | Main idea to extract |
| --- | --- | --- | --- |
| Roofline | https://jax-ml.github.io/scaling-book/roofline/ | Week 7 kernel/performance and Week 9 Pallas | Decide whether a workload is compute-bound, memory-bandwidth-bound, or communication-bound. |
| TPUs | https://jax-ml.github.io/scaling-book/tpus/ | Week 9 TPU/JAX/XLA | Understand TPU execution, memory, and why TPU thinking differs from GPU thinking. |
| GPUs | https://jax-ml.github.io/scaling-book/gpus/ | Week 7 GPU basics | Connect GPU architecture to practical performance limits. |
| Sharding | https://jax-ml.github.io/scaling-book/sharding/ | Week 1 distributed training map, Week 8 collectives, Week 9 XLA | Understand how arrays and computation are partitioned and where communication appears. |
| Transformers | https://jax-ml.github.io/scaling-book/transformers/ | Week 4 training memory and Week 9 HLO notes | Connect transformer operations to memory, compute, and compiler/runtime behavior. |
| Training | https://jax-ml.github.io/scaling-book/training/ | Week 4 distributed training | Understand model state, activation memory, batch/sequence scaling, and throughput tradeoffs. |
| Applied Training | https://jax-ml.github.io/scaling-book/applied-training/ | Week 9 profiling/training debug and Week 11 reliability | Turn training theory into performance/debugging questions. |
| Inference | https://jax-ml.github.io/scaling-book/inference/ | Week 5 SGLang/vLLM serving | Understand prefill, decode, KV cache pressure, latency, and throughput. |
| Applied Inference | https://jax-ml.github.io/scaling-book/applied-inference/ | Week 5 serving project and SGLang contribution track | Connect serving theory to benchmarks and operational tradeoffs. |
| Profiling | https://jax-ml.github.io/scaling-book/profiling/ | Week 7 profiler work and Week 9 JAX artifact | Learn what to measure before guessing at performance bottlenecks. |
| JAX | https://jax-ml.github.io/scaling-book/jax-stuff/ | Week 9 JAX/XLA/Pallas | Understand why JAX transformations and lowering matter for accelerator systems. |

## Where It Enters The 12-Week Plan

| Week | Day | Reading | Artifact impact |
| --- | --- | --- | --- |
| Week 1 | Day 6 | Sharding intro | Better architecture diagram for distributed training. |
| Week 4 | Day 2 | Transformers + Training | Better memory estimator and clearer model-state categories. |
| Week 5 | Day 4 | Inference + Applied Inference intros | Better TTFT/ITL/goodput definitions and serving simulator metrics. |
| Week 7 | Day 1 | Roofline + GPUs intros | Better kernel benchmark framing. |
| Week 8 | Day 2 | Sharding communication sections | Better scaling-efficiency calculator and collective mental model. |
| Week 9 | Days 1-7 | JAX, Roofline, TPUs, Sharding, Transformers, Profiling, Applied Training | Main reference for the JAX/XLA/Pallas project. |

## How To Read It In One Hour

For each assigned chapter:

1. Spend 5 minutes reading the chapter outline and diagrams.
2. Spend 15 minutes reading the first conceptual section carefully.
3. Spend 15 minutes reading one formula, table, or worked example.
4. Spend 15 minutes writing a concrete mapping to the weekly artifact.
5. Spend 10 minutes answering the checkpoint and committing the note.

## Checkpoint Prompts

Use these when a daily guide does not provide a more specific question.

### Roofline

What resource is the bottleneck: compute, memory bandwidth, communication, or launch/host overhead? What measurement would prove it?

### Sharding

Which tensor or computation is split, across which axis, and what communication does that split introduce?

### Training

Which memory category grows with model size, batch size, sequence length, or optimizer choice?

### Inference

Is the current bottleneck prefill, decode, KV cache memory, batching, or scheduling? Which metric would expose it?

### Profiling

What should be measured before changing code, and what would count as evidence that the change helped?

### JAX/XLA/Pallas

What does the high-level JAX code become after transformation/lowering, and where can the compiler or kernel author improve execution?

## Portfolio Tie-In

Use this source explicitly in these READMEs:

- `03-kv-cache-serving/README.md`: cite inference and applied inference for prefill/decode, KV cache, TTFT/ITL/goodput.
- `05-kernel-bench/README.md`: cite roofline, GPUs, and profiling for benchmark interpretation.
- `06-jax-xla-pallas/README.md`: cite JAX, TPUs, sharding, StableHLO/OpenXLA, and profiling.

Do not write "I read the JAX Scaling Book." Instead, show the idea in an artifact:

- A memory formula.
- A roofline-style benchmark interpretation.
- A sharding diagram.
- A prefill/decode metric table.
- A profiler note that changes what you would optimize next.
