# AI Infrastructure Transition Study Plan - 1 Hour Daily

Purpose: move from a traditional data science / DevOps profile into AI infrastructure work across cluster/platform engineering, distributed training, inference systems, accelerator systems, and performance engineering.

The RadixArk postings that inspired this plan are reference examples only. Use them to understand what modern AI infrastructure teams care about; do not treat them as the final target company, the only acceptable job family, or daily study material.

Track priority from your resume:

1. Cluster / Platform: closest fit. Your Kubernetes, Kubeflow, AWS, observability, CI/CD, platform, and production AI service experience already maps well.
2. Training: also close. You already have fine-tuning SDK, benchmarking, agent experiments, RAG, and ML platform work. The missing pieces to make public are distributed training internals, post-training/RL infrastructure, checkpointing, and failure recovery.
3. TPU Systems: stretch but reachable as a portfolio lane. You need a visible JAX/XLA/Pallas artifact.
4. Kernel / Compiler / Communication: deepest gap. Treat this as a 6 to 12 month specialization track. The 12-week plan below creates credible proof, but not mastery.

Primary open-source target: SGLang. Treat vLLM as an important comparison source, but make SGLang the repo where you build repeated contribution history. The six-month goal is to become a trusted recurring contributor with multiple merged PRs, useful issue triage, reproducible benchmarks, and subsystem familiarity. Official maintainer status is possible but not fully under your control, so do not use it as the only success metric.

The plan uses 1 hour per day:

- 10 minutes: source-grounded recall from yesterday, written in `checkpoints/week-N.md`.
- 25 minutes: read or watch the exact assigned material.
- 20 minutes: implement, profile, draw, or document one small artifact.
- 5 minutes: commit notes, update README, or draft one LinkedIn sentence.

Add a SGLang open-source lane without increasing daily study time:

- Daily minimum: spend 10 minutes reading one SGLang issue, PR, source file, test, or docs page.
- Weekly minimum: reserve one full 60-minute session for SGLang contribution work.
- Rule: do not wait until Week 12 to engage. Week 12 is for packaging and outreach, not first contact with the repo.

## Source Catalog

Use university courses, official docs, and widely used project docs/blogs as the primary sources.

Calibration examples to read once before starting, then revisit only when you are packaging your work for applications:

- RadixArk Cluster / Platform job: https://job-boards.greenhouse.io/radixark/jobs/4134836009
- RadixArk Training job: https://job-boards.greenhouse.io/radixark/jobs/4134907009
- RadixArk Kernel / Compiler / Communication job: https://job-boards.greenhouse.io/radixark/jobs/4134913009
- RadixArk TPU Systems job: https://job-boards.greenhouse.io/radixark/jobs/4087890009

Primary study sources:

- MIT 6.5840 Distributed Systems: https://pdos.csail.mit.edu/6.824/
- MIT 6.5840 Schedule: https://pdos.csail.mit.edu/6.824/schedule.html
- Stanford CS149 Parallel Computing: https://cs149.stanford.edu/
- Stanford CS149 Fall 2023 schedule: https://cs149.stanford.edu/fall23
- CMU 11-868 LLM Systems: https://llmsystem.github.io/llmsystem2025spring/
- Stanford CS336 Language Modeling from Scratch: https://cs336.stanford.edu/spring2025/
- Stanford CS336 Spring 2025 lecture repo: https://github.com/stanford-cs336/spring2025-lectures
- Stanford CS336 Lecture 10 inference code: https://github.com/stanford-cs336/spring2025-lectures/blob/main/lecture_10.py
- Hugging Face Ultra-Scale Playbook: https://nanotron-ultrascale-playbook.static.hf.space/
- PyTorch FSDP2 tutorial: https://docs.pytorch.org/tutorials/intermediate/FSDP_tutorial.html
- PyTorch Distributed Checkpoint docs: https://docs.pytorch.org/docs/stable/distributed.checkpoint.html
- TorchTitan: https://github.com/pytorch/torchtitan
- SGLang GitHub: https://github.com/sgl-project/sglang
- SGLang docs: https://docs.sglang.io/
- SGLang contribution guide: https://docs.sglang.io/docs/developer_guide/contribution_guide
- SGLang developer overview: https://docs.sglang.io/docs/developer_guide/overview
- SGLang benchmark and profiling guide: https://docs.sglang.io/docs/developer_guide/benchmark_and_profiling
- SGLang serving benchmark guide: https://docs.sglang.io/docs/developer_guide/bench_serving
- SGLang RadixAttention concept: https://sgl-project-sglang-93.mintlify.app/concepts/radix-attention
- SGLang paper/blog: https://www.lmsys.org/blog/2024-01-17-sglang/
- vLLM docs: https://docs.vllm.ai/
- vLLM PagedAttention blog: https://vllm.ai/blog/2023-06-20-vllm
- Kubernetes Device Plugins: https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/device-plugins/
- Kubernetes GPU scheduling: https://kubernetes.io/docs/tasks/manage-gpus/scheduling-gpus/
- Kubernetes Scheduling Framework: https://kubernetes.io/docs/concepts/scheduling-eviction/scheduling-framework/
- Kubernetes Priority and Preemption: https://kubernetes.io/docs/concepts/scheduling-eviction/pod-priority-preemption/
- Kubernetes Node-pressure Eviction: https://kubernetes.io/docs/concepts/scheduling-eviction/node-pressure-eviction/
- Kueue overview: https://kueue.sigs.k8s.io/docs/overview/
- Kueue ResourceFlavor: https://kueue.sigs.k8s.io/docs/concepts/resource_flavor/
- Kueue ClusterQueue: https://kueue.sigs.k8s.io/docs/concepts/cluster_queue/
- Kueue Workload: https://kueue.sigs.k8s.io/docs/concepts/workload/
- Volcano unified scheduling: https://volcano.sh/docs/keyfeatures/unifiedscheduling/
- Slurm GRES GPU scheduling: https://slurm.schedmd.com/gres.html
- Ray resources and scheduling: https://docs.ray.io/en/latest/ray-core/scheduling/resources.html
- KubeRay GPU guide: https://docs.ray.io/en/latest/cluster/kubernetes/user-guides/gpu.html
- NVIDIA CUDA Programming Guide: https://docs.nvidia.com/cuda/cuda-programming-guide/index.html
- NVIDIA CUDA C++ intro: https://docs.nvidia.com/cuda/cuda-programming-guide/02-basics/intro-to-cuda-cpp.html
- NVIDIA NCCL docs: https://docs.nvidia.com/deeplearning/nccl/user-guide/docs/
- NVIDIA NCCL overview: https://docs.nvidia.com/deeplearning/nccl/user-guide/docs/overview.html
- JAX Pallas quickstart: https://docs.jax.dev/en/latest/pallas/quickstart.html
- JAX Pallas docs: https://docs.jax.dev/en/latest/pallas/index.html
- JAX Pallas TPU docs: https://docs.jax.dev/en/latest/pallas/tpu/
- OpenXLA XLA overview: https://openxla.org/xla
- OpenXLA GPU architecture: https://openxla.org/xla/gpu_architecture
- OpenXLA StableHLO spec: https://openxla.org/stablehlo/spec
- JAX Scaling Book main: https://jax-ml.github.io/scaling-book/
- JAX Scaling Book roofline: https://jax-ml.github.io/scaling-book/roofline/
- JAX Scaling Book TPUs: https://jax-ml.github.io/scaling-book/tpus/
- JAX Scaling Book GPUs: https://jax-ml.github.io/scaling-book/gpus/
- JAX Scaling Book sharding: https://jax-ml.github.io/scaling-book/sharding/
- JAX Scaling Book transformers: https://jax-ml.github.io/scaling-book/transformers/
- JAX Scaling Book training: https://jax-ml.github.io/scaling-book/training/
- JAX Scaling Book applied training: https://jax-ml.github.io/scaling-book/applied-training/
- JAX Scaling Book inference: https://jax-ml.github.io/scaling-book/inference/
- JAX Scaling Book applied inference: https://jax-ml.github.io/scaling-book/applied-inference/
- JAX Scaling Book profiling: https://jax-ml.github.io/scaling-book/profiling/
- JAX Scaling Book JAX chapter: https://jax-ml.github.io/scaling-book/jax-stuff/
- Brendan Gregg USE method: https://www.brendangregg.com/USEmethod/use-linux.html
- Brendan Gregg Linux performance: https://www.brendangregg.com/linuxperf.html
- Linux perf wiki: https://perfwiki.github.io/main/
- OpenTelemetry traces concept: https://opentelemetry.io/docs/concepts/signals/traces/
- OpenTelemetry metrics concept: https://opentelemetry.io/docs/concepts/signals/metrics/
- verl docs: https://verl.readthedocs.io/
- verl GitHub: https://github.com/verl-project/verl
- OpenRLHF docs: https://openrlhf.readthedocs.io/
- Hugging Face TRL docs: https://huggingface.co/docs/trl/en/index

## Portfolio Outcomes

Create one GitHub organization-level portfolio repo or six small repos. A single repo is easier to maintain:

`ai-infra-transition-lab/`

- `01-cluster-scheduler/`: simulator for GPU/TPU queues, quota, preemption, gang scheduling, and utilization.
- `02-training-reliability/`: tiny distributed training job with FSDP/DDP options, checkpoint/resume, and fault injection.
- `03-kv-cache-serving/`: PagedAttention-style block allocator plus RadixAttention-style prefix cache simulator.
- `04-post-training-rollouts/`: async rollout harness for DPO/GRPO-style post-training with reward execution and metrics.
- `05-kernel-bench/`: CUDA/Triton or PyTorch extension benchmark for layernorm, matmul, softmax, or attention-adjacent kernels.
- `06-jax-xla-pallas/`: Pallas kernel, JAXPR/HLO dump, StableHLO annotation, and SPMD/sharding notes.

Each folder should have:

- `README.md` with problem, source material, design, results, and what you would do at 1000+ GPU scale.
- `notes.md` with the daily checkpoint answers.
- `benchmarks/` with CSV or JSON outputs.
- `diagrams/` with one architecture diagram.
- A LinkedIn post draft of 150 to 250 words.

## Daily Guides

Some days need more than a link list. When a day has a guide, follow that guide first; it contains the exact reading range, learning objective, checkpoint questions, and artifact template for that hour.

- Week 1 Day 1: `daily_guides/week_01_day_01_ai_infra_stack.md`
- Week 1 Day 2: `daily_guides/week_01_day_02_distributed_systems_spine.md`
- Week 1 Day 3: `daily_guides/week_01_day_03_mapreduce_training_pipeline.md`
- Week 1 Day 4: `daily_guides/week_01_day_04_gfs_checkpoint_manifest.md`
- SGLang six-month open-source lane: `open_source/sglang_contribution_track.md`
- JAX Scaling Book reading map: `reading_maps/jax_scaling_book.md`

## Checkpoint Rules

Every future lesson should separate what the source directly teaches from what the artifact or broader study plan asks you to infer. This avoids the Day 1 problem where a question felt like it should come from one reading but actually required broader synthesis.

Use these tags in every daily guide and checkpoint file:

- `Source-grounded`: answer only from the assigned reading/video/doc section.
- `Artifact-grounded`: answer from the code, table, diagram, benchmark, or note you built that day.
- `Synthesis`: a first-pass connection across multiple layers of the AI infrastructure stack. It is okay to mark this as `TODO` or low confidence.
- `Prior experience`: answer from your production background, then revise after later lessons.

If a question cannot be answered from the assigned source, label it `Synthesis` or `Prior experience`; do not pretend the source covered it.

The weekly tables now tag each checkpoint prompt with the expected evidence source, such as `Source-grounded`, `Artifact-grounded`, or `Synthesis`.

## Week 1 - AI Infrastructure Stack and Distributed Systems Spine

Goal: build a concrete technical map of the AI infrastructure stack, then refresh distributed systems vocabulary.

| Day | 60-minute assignment | Concept to learn | Checkpoint | Build artifact |
| --- | --- | --- | --- | --- |
| 1 | Follow `daily_guides/week_01_day_01_ai_infra_stack.md`: read the Ultra-Scale Playbook high-level overview and first memory-accounting sections, then skim CS336 assignments/schedule to map the systems topics. | Why AI infrastructure exists: memory, compute, communication, scheduling, and reliability constraints. | Source-grounded + synthesis: Why is large-model training an infrastructure problem, not just a modeling problem? | `notes/week_01/day_01_stack_map.md`: AI infrastructure stack map and bottleneck table. |
| 2 | Follow `daily_guides/week_01_day_02_distributed_systems_spine.md`: read MIT 6.5840 home page and Lecture 1, then read Google Research "The Tail at Scale" summary for tail latency. | Failure models, replication, consistency, scalability, and tail latency. | Source-grounded + synthesis: define distributed system, availability, consistency, fault tolerance, scalability, and tail latency, then map them to AI infrastructure. | `notes/distributed-systems-glossary.md`. |
| 3 | Follow `daily_guides/week_01_day_03_mapreduce_training_pipeline.md`: read MIT 6.5840 Lab 1 context and the MapReduce paper sections on programming model, execution overview, fault tolerance, locality, task granularity, and backup tasks. | Task scheduling, stragglers, retry, data locality. | Source-grounded + artifact-grounded: Why is a straggler different from a failed task, and how does that map to AI data pipeline reliability? | `notes/week_01/day_03_mapreduce_training_pipeline.md`: MapReduce concept map and AI training data pipeline sketch. |
| 4 | Follow `daily_guides/week_01_day_04_gfs_checkpoint_manifest.md`: read MIT 6.5840 GFS context and the GFS paper sections on architecture, single master, metadata, operation log, checkpoints, leases, and self-validating records. | Metadata master, chunk placement, leases, checkpoint storage. | Source-grounded + artifact-grounded: what metadata does GFS centralize, and what metadata must a training checkpoint store to be resumable? | `artifacts/week_01/checkpoint_manifest.json` plus `notes/week_01/day_04_gfs_checkpoint_manifest.md`. |
| 5 | Read MIT 6.5840 Raft lecture/paper from the schedule. | Leader election, log replication, control-plane consensus. | Source-grounded: Why is scheduler state harder than stateless API serving? | Draw a scheduler control-plane failure diagram. |
| 6 | Read the Ultra-Scale Playbook sections on data parallelism, tensor parallelism, pipeline parallelism, sequence parallelism, and context parallelism. Then read the JAX Scaling Book sharding chapter intro as a second explanation of the same idea. | How distributed training splits work across devices. | Source-grounded: Which parallelism strategy reduces which bottleneck, and what communication does it introduce? | Architecture diagram: "large-model training platform". |
| 7 | Weekly review. Rewrite your resume headline and top 6 bullets for AI infrastructure. | Career positioning. | Synthesis: Can each bullet prove systems depth, scale, and reliability? | LinkedIn draft: "Why I am moving into AI infrastructure". |

## Week 2 - GPU/TPU Cluster Scheduling

Goal: show you understand how AI workloads get admitted, placed, preempted, and observed.

| Day | 60-minute assignment | Concept to learn | Checkpoint | Build artifact |
| --- | --- | --- | --- | --- |
| 1 | Read Kubernetes Device Plugins and GPU Scheduling. | Extended resources, device plugin lifecycle, GPU limits. | Source-grounded: Why are GPUs requested through `limits`, not normal CPU-style requests? | Define `Node`, `Device`, `Workload` classes. |
| 2 | Read Kubernetes Scheduling Framework. | Filter, score, bind, scheduling plugins. | Source-grounded: What is the difference between filter and score? | Implement first-fit placement in `01-cluster-scheduler`. |
| 3 | Read Kubernetes Priority and Preemption. | Priority classes, eviction, starvation risk. | Source-grounded: When can preemption make utilization worse? | Add priority and preemption to simulator. |
| 4 | Read Kueue overview plus ClusterQueue and Workload concept docs. | Quotas, admission control, fair sharing. | Source-grounded: Why does AI batch scheduling often need job-level admission? | Add team quota and fair share queues. |
| 5 | Read Volcano unified scheduling and KubeRay Volcano integration. | Gang scheduling for distributed jobs. | Source-grounded: Why can partial pod scheduling waste expensive GPUs? | Add gang scheduling and pending reasons. |
| 6 | Read Slurm GRES and Ray resources. | HPC GPU allocation, custom resources, Ray actor placement. | Source-grounded: Compare Slurm GRES, Kubernetes device plugins, and Ray resources. | Add a scheduler comparison table. |
| 7 | Ship project slice 1. | Cluster/platform artifact quality. | Artifact-grounded: What three metrics convince a platform team your scheduler is useful? | README with utilization plots and one runbook. |

## Week 3 - Linux, Networking, and Observability

Goal: build the debugging instincts needed for hardware, OS, networking, and distributed AI services.

| Day | 60-minute assignment | Concept to learn | Checkpoint | Build artifact |
| --- | --- | --- | --- | --- |
| 1 | Read Brendan Gregg USE method. | Utilization, saturation, errors. | Source-grounded: For GPU, CPU, memory, disk, NIC: what are U/S/E metrics? | Add `observability/use-checklist.md`. |
| 2 | Read Brendan Gregg Linux performance overview. | Workload characterization and bottleneck thinking. | Source-grounded: What changed? What is the latency metric? What is saturation? | Create incident template for failed training jobs. |
| 3 | Read Linux perf wiki intro. | Sampling profiler, counters, flame graphs. | Source-grounded: Why can CPU profiling still matter for GPU workloads? | Profile a Python CPU hot loop and save output. |
| 4 | Read OpenTelemetry traces and metrics concept pages. | Traces, metrics, logs, cardinality. | Source-grounded: Which labels are dangerous at AI cluster scale? | Metrics schema for scheduler simulator. |
| 5 | Read NVIDIA NCCL overview. | Collective communication, topology awareness. | Source-grounded: What does all-reduce do during data-parallel training? | Add "network and collective" section to runbook. |
| 6 | Read Kubernetes Node-pressure Eviction. | Node-level pressure, eviction, reliability. | Source-grounded: What happens when disk, memory, or PID pressure occurs? | Add failure injection cases to simulator. |
| 7 | Ship project slice 2. | Operational credibility. | Artifact-grounded: Can a reader reproduce one failure and see one metric change? | LinkedIn draft: "How I debug AI cluster failures". |

## Week 4 - Distributed Training with PyTorch

Goal: make distributed training memory, communication, checkpointing, and throughput visible.

| Day | 60-minute assignment | Concept to learn | Checkpoint | Build artifact |
| --- | --- | --- | --- | --- |
| 1 | Read PyTorch FSDP2 tutorial through "How FSDP2 works". | DDP versus FSDP, sharding parameters/gradients/optimizer state. | Source-grounded: Why does FSDP reduce memory versus DDP? | Create tiny transformer training script. |
| 2 | Read Hugging Face Ultra-Scale Playbook sections on data parallelism and ZeRO/FSDP. Then read JAX Scaling Book transformers and training chapter sections on model state, activation memory, and scaling tradeoffs. | Parallelism taxonomy and memory accounting. | Source-grounded: Where do parameters, gradients, activations, and optimizer state live, and which parts scale with batch size or sequence length? | Add memory-estimator notebook. |
| 3 | Read TorchTitan README. | Native PyTorch large-scale training stack. | Source-grounded: What does TorchTitan expose that a platform engineer should understand? | Add TorchTitan architecture notes. |
| 4 | Run DDP locally with CPU/Gloo. If the machine has a CUDA GPU, repeat once with GPU/NCCL and compare notes. | Process groups, ranks, world size. | Artifact-grounded: What do rank, local rank, and world size mean? | Save throughput metrics to CSV. |
| 5 | Add FSDP option or document a CPU-compatible simulation if no GPU. | Shard lifecycle and all-gather timing. | Artifact-grounded: Why can FSDP introduce communication overhead? | CLI flag: `--strategy ddp|fsdp|single`. |
| 6 | Read PyTorch Distributed Checkpoint docs, then add checkpoint and resume. | Fault tolerance for long training jobs. | Source-grounded: What state must be saved besides model weights? | Kill and resume demo in README. |
| 7 | Ship project slice 3. | Training systems proof. | Artifact-grounded: Can someone see tokens/sec, memory estimate, and recovery behavior? | LinkedIn draft: "Small-scale reproduction of large-scale training problems". |

## Week 5 - SGLang-First LLM Serving, KV Cache, and vLLM Comparison

Goal: understand inference performance from the system side, especially SGLang runtime design, KV cache behavior, batching, prefix reuse, and where vLLM provides useful comparison.

| Day | 60-minute assignment | Concept to learn | Checkpoint | Build artifact |
| --- | --- | --- | --- | --- |
| 1 | Read SGLang docs overview, developer overview, and contribution guide sections on source install, pre-commit, unit tests, docs, accuracy tests, speed benchmarks, review, CI, code style, and newcomer tips. | SGLang as both runtime and open-source project. | Source-grounded: What does SGLang expect from a useful contributor before review? | `open_source/sglang_repo_map.md`: top-level repo map, test paths, and first subsystem candidates. |
| 2 | Read SGLang paper/blog and docs overview. | Low-latency/high-throughput serving, runtime design, structured generation. | Source-grounded: What problem does SGLang solve that a plain model API does not? | Add request simulator with arrival times. |
| 3 | Read SGLang RadixAttention concept and inspect related docs/issues. | Prefix tree cache and reuse. | Source-grounded + synthesis: When does prefix caching help most, and which workloads in your experience match that pattern? | Implement radix prefix lookup and LRU eviction. |
| 4 | Read Stanford CS336 Spring 2025 `lecture_10.py` on inference, then read JAX Scaling Book inference and applied inference intros. | Inference bottlenecks and serving metrics. | Source-grounded: Define TTFT, ITL, throughput, goodput, prefill, decode, and KV cache pressure. | Add metrics output for simulated serving. |
| 5 | Read vLLM PagedAttention blog as comparison, then compare it to SGLang RadixAttention. | Block allocation versus prefix-aware reuse. | Synthesis: Are these competing or complementary ideas? | Write design note with diagrams. |
| 6 | SGLang hands-on if hardware permits: run a small local model or run docs/tests/benchmarks that do not require a large GPU. If not, create a reproducible benchmark plan only. | Practical serving tradeoffs and contributor workflow. | Artifact-grounded: What can you reproduce locally, and what requires GPU/cloud access? | Save benchmark table or benchmark plan. |
| 7 | Ship project slice 4 and pick one SGLang issue or docs/test improvement candidate. | Inference systems artifact plus first contribution target. | Artifact-grounded: Can the README explain why agent workloads benefit from prefix caching and point to one realistic SGLang contribution? | LinkedIn draft: "KV cache as a systems problem"; update `open_source/sglang_contribution_track.md`. |

## Week 6 - Post-Training and Agentic RL Infrastructure

Goal: connect your agent background to modern post-training infrastructure: async rollouts, sandboxing, reward execution, observability, and reliability.

| Day | 60-minute assignment | Concept to learn | Checkpoint | Build artifact |
| --- | --- | --- | --- | --- |
| 1 | Read Hugging Face TRL overview and DPO trainer docs. | SFT, DPO, reward modeling, preference optimization. | Source-grounded: How is DPO different from PPO-style RLHF? | Minimal DPO data schema. |
| 2 | Read TRL GRPO trainer docs. | GRPO and reasoning/post-training workflows. | Source-grounded: Why can GRPO avoid a separate value model? | Reward function interface. |
| 3 | Read verl docs overview. | Production-ready RL post-training framework. | Source-grounded: What pieces exist in an RL post-training pipeline? | Draw actor, rollout, reward, trainer diagram. |
| 4 | Read OpenRLHF docs overview. | Ray + vLLM + DeepSpeed architecture. | Source-grounded: Why is generation often the RLHF bottleneck? | Async rollout queue skeleton. |
| 5 | Implement a tiny reward harness for math or code-format tasks. | Sandboxed rewards and determinism. | Artifact-grounded: What makes a reward function exploitable? | `reward.py` plus unit tests. |
| 6 | Add metrics: rollout latency, reward pass rate, retry count, queue depth. | Observability for post-training jobs. | Artifact-grounded: Which metric tells you rollout is starving training? | Dashboard JSON or simple plots. |
| 7 | Ship project slice 5. | Training-role proof. | Artifact-grounded: Can a reviewer see you understand agentic post-training infra? | LinkedIn draft: "Agentic post-training is a distributed systems problem". |

## Week 7 - CUDA, Triton, and Performance Basics

Goal: create honest kernel/performance proof without pretending to be a compiler engineer yet.

| Day | 60-minute assignment | Concept to learn | Checkpoint | Build artifact |
| --- | --- | --- | --- | --- |
| 1 | Read Stanford CS149 lecture 7 material on GPU architecture/CUDA from Fall 2023, then read JAX Scaling Book roofline intro and GPU chapter intro. | SIMT, warps, memory hierarchy, occupancy, roofline thinking. | Source-grounded: What is a warp? What causes divergence? What does roofline analysis ask about compute versus memory bandwidth? | `05-kernel-bench/notes/gpu-basics.md`. |
| 2 | Read NVIDIA CUDA C++ intro. | Host/device, kernel launch, memory copy. | Source-grounded: Why is host-device transfer often a bottleneck? | Vector add or PyTorch extension plan. |
| 3 | Read CUDA Programming Guide performance sections at a high level. | Coalescing, shared memory, occupancy. | Source-grounded: What is memory coalescing? | Add benchmark harness with timing utility. |
| 4 | Implement or adapt a simple CUDA/Triton kernel if hardware supports it. If not, use PyTorch CPU/GPU baselines and write the kernel as documented code. | Kernel correctness and benchmarking. | Artifact-grounded: Why must benchmarks warm up? | Save baseline timings. |
| 5 | Implement layernorm, softmax, or matmul microbenchmark. | Arithmetic intensity and memory bandwidth. | Artifact-grounded: Which operation is memory-bound, and why? | Plot runtime vs tensor size. |
| 6 | Use PyTorch profiler on the benchmark. If Nsight Systems is installed, run one additional Nsight capture and compare timelines. | Profiling timelines and kernel attribution. | Artifact-grounded: What does profiler overhead change? | Add profiler screenshot or text output. |
| 7 | Ship project slice 6. | Kernel credibility. | Artifact-grounded: Can a reader reproduce the benchmark and understand the bottleneck? | LinkedIn draft: "My first AI kernel benchmark". |

## Week 8 - Collectives, NCCL, and High-Speed Interconnects

Goal: bridge training systems and cluster/platform work through communication primitives.

| Day | 60-minute assignment | Concept to learn | Checkpoint | Build artifact |
| --- | --- | --- | --- | --- |
| 1 | Read NVIDIA NCCL overview and "Using NCCL". | All-reduce, broadcast, reduce-scatter, all-gather. | Source-grounded: Which collective appears in DDP? Which appears in FSDP? | Collective glossary. |
| 2 | Read Hugging Face Ultra-Scale Playbook communication sections, then read JAX Scaling Book sharding sections on communication and partitioning. | Communication/computation overlap, sharding, and bottlenecks. | Source-grounded: Why does scaling efficiency drop as GPU count grows, and how does sharding introduce communication? | Add scaling-efficiency calculator. |
| 3 | Implement ring all-reduce simulator in Python. | Latency, bandwidth, chunking. | Artifact-grounded: How many steps does ring all-reduce need for N ranks? | `ring_allreduce_sim.py`. |
| 4 | Read Slurm GRES again with NCCL mental model. | Scheduling topology-aware workloads. | Source-grounded: Why might two 8-GPU jobs perform differently on the same cluster? | Add topology field to scheduler simulator. |
| 5 | Read Kubernetes Scheduling Framework scoring extension points and Volcano unified scheduling, then design a topology-aware scoring rule. | Topology-aware placement. | Source-grounded: What placement constraints improve all-reduce? | Add topology-aware scoring. |
| 6 | Write incident: "training throughput dropped 40 percent after reschedule". | Cross-layer debugging. | Synthesis: What data do you gather from app, NCCL, node, scheduler, and network? | Runbook with hypotheses and checks. |
| 7 | Ship communication milestone. | Kernel, training, and cluster bridge. | Artifact-grounded: Can you explain RDMA/InfiniBand/NVLink/NCCL without hand-waving? | LinkedIn draft: "Collectives are where ML meets infrastructure". |

## Week 9 - JAX, XLA, StableHLO, and Pallas

Goal: use the JAX Scaling Book as the spine for a visible TPU/JAX/XLA artifact, even if you do not have TPU access.

| Day | 60-minute assignment | Concept to learn | Checkpoint | Build artifact |
| --- | --- | --- | --- | --- |
| 1 | Read JAX Scaling Book JAX chapter intro and JAX Pallas quickstart. | JAX mental model plus lower-level kernel control. | Source-grounded: How is Pallas lower-level than normal JAX, and why does JAX expose transformations instead of only eager execution? | `06-jax-xla-pallas/pallas_vector_add.py`. |
| 2 | Read JAX Scaling Book roofline chapter and JAX Pallas docs overview. | Kernel language mental model and performance ceilings. | Source-grounded: What control does Pallas give you that XLA usually hides, and what does roofline thinking say to measure first? | Add annotated kernel comments and expected bottleneck note. |
| 3 | Read JAX Scaling Book TPUs chapter and JAX Pallas TPU docs overview. | TPU memory spaces, pipelining, TPU-specific constraints. | Source-grounded: What changes between GPU and TPU kernel thinking? | TPU notes: "what I can test locally vs on TPU". |
| 4 | Read JAX Scaling Book sharding chapter and OpenXLA XLA overview. | ML compiler pipeline, sharding, and accelerator targets. | Source-grounded: What problem does XLA solve, and why does sharding force communication decisions? | Dump and save `jaxpr` and HLO if possible. |
| 5 | Read JAX Scaling Book transformers chapter and OpenXLA StableHLO spec introduction. | Transformer computation as compiler/runtime work. | Source-grounded: Why does StableHLO matter for compiler ecosystems, and which transformer operations dominate memory or compute? | Annotate 5 HLO ops from your toy model. |
| 6 | Read JAX Scaling Book profiling and applied training chapters. | Profiling, SPMD, communication insertion, and training performance debugging. | Source-grounded: What is the difference between data, tensor, and pipeline parallelism, and what would you profile first? | Sharding strategy and profiling note. |
| 7 | Ship TPU/JAX milestone with the JAX Scaling Book as the main reference. | TPU Systems proof. | Artifact-grounded: Can a reader see Pallas code, compiler artifact, sharding reasoning, and performance/debugging logic? | LinkedIn draft: "Learning JAX/XLA/Pallas from a systems angle". |

## Week 10 - Capacity Planning, Multi-Tenant Scheduling, and Cost

Goal: make Cluster/Platform work feel like production resource management, not just Kubernetes familiarity.

| Day | 60-minute assignment | Concept to learn | Checkpoint | Build artifact |
| --- | --- | --- | --- | --- |
| 1 | Read Kueue resource flavor and ClusterQueue docs, then define a capacity model for a mixed GPU/TPU cluster. | Utilization, reliability, capacity planning. | Source-grounded: What is the difference between allocation, reservation, and utilization? | Capacity planning spreadsheet or CSV model. |
| 2 | Read Kueue workload and ClusterQueue concepts. | Admission, quota, local queue, cluster queue. | Source-grounded: Why should queued jobs not create pods immediately? | Add admission decision logs. |
| 3 | Read Ray scheduling resources and KubeRay GPU guide. | Application-level scheduling and GPU actors. | Source-grounded: When would you use Ray placement instead of only Kubernetes scheduling? | Add Ray-style actor workload type. |
| 4 | Read Volcano unified scheduling. | Queue, gang, fair share, topology. | Source-grounded: What problem does gang scheduling solve that priority does not? | Add gang fairness test cases. |
| 5 | Build a synthetic workload trace: training jobs, inference pods, RL rollout jobs. | Mixed workload economics. | Artifact-grounded: Which workload is preemptible? Which has SLO? | Generate utilization chart. |
| 6 | Write "preempt training for inference" policy and failure modes. | Reliability and product tradeoffs. | Synthesis: How can preemption hurt checkpoint cost? | Policy doc plus simulator comparison. |
| 7 | Ship cluster platform capstone. | Cluster/platform application proof. | Artifact-grounded: Does the README make the scheduling tradeoffs clear to a platform engineer who has never met you? | LinkedIn draft: "AI cluster scheduling under mixed workloads". |

## Week 11 - Reliability, Fault Recovery, and Long-Running Jobs

Goal: demonstrate that you can keep expensive jobs alive and explain failure recovery clearly.

| Day | 60-minute assignment | Concept to learn | Checkpoint | Build artifact |
| --- | --- | --- | --- | --- |
| 1 | Revisit MIT 6.5840 fault-tolerance topics and your Week 4 checkpoint code. | Failure domains and recovery semantics. | Source-grounded: What does exactly-once mean for training checkpoints? | Add failure-domain table. |
| 2 | Add failure injection to training script: kill at step N, resume from latest checkpoint. | Recovery testing. | Artifact-grounded: How do you prove no data duplication or lost steps? | `--fail-at-step` demo. |
| 3 | Add metric: time to recover, lost work, checkpoint size, checkpoint interval. | Reliability SLOs. | Artifact-grounded: What checkpoint interval minimizes expected lost work? | Recovery results CSV. |
| 4 | Write incident: "worker OOM during RL rollout generation". | Cross-layer incident response. | Synthesis: Which component owns the failure: model, serving, scheduler, or platform? | Incident report template. |
| 5 | Add queue retry/backoff policy in rollout harness. | Retry storms and backpressure. | Artifact-grounded: How can retries make outage worse? | Backoff implementation. |
| 6 | Create final architecture diagram tying scheduler, training, serving, rollouts, observability. | End-to-end AI infra. | Artifact-grounded: Where are the control plane and data plane? | `diagrams/end_to_end_ai_infra.md`. |
| 7 | Ship reliability milestone. | Training + platform maturity. | Artifact-grounded: Can a hiring manager see production judgment? | LinkedIn draft: "Fault tolerance in long-running AI jobs". |

## Week 12 - Open Source, Interview Story, and Public Launch

Goal: convert study into evidence: GitHub, LinkedIn, resume bullets, SGLang contribution proof, and interview narratives.

| Day | 60-minute assignment | Concept to learn | Checkpoint | Build artifact |
| --- | --- | --- | --- | --- |
| 1 | Revisit the SGLang contribution guide, your Week 5 repo map, and five recent SGLang issues/PRs in your chosen subsystem. | Open-source contribution strategy. | Synthesis: What issue is small, reproducible, useful, and aligned with maintainer priorities? | `open_source/sglang_issue_shortlist.md`. |
| 2 | Make one SGLang docs improvement, test improvement, repro script, benchmark issue, or small PR locally. | Maintainer empathy. | Artifact-grounded: What evidence would make this issue easy to triage? | Draft SGLang issue/PR text. |
| 3 | Revise resume summary and top 8 bullets toward AI infrastructure. | Narrative compression. | Synthesis: Does each bullet show scale, system, and outcome? | `resume_ai_infra_bullets.md`. |
| 4 | Prepare interview stories: cluster outage, training failure, inference bottleneck, open-source contribution. | STAR stories for systems roles. | Synthesis: What was the constraint, tradeoff, and measurable result? | `interview_story_bank.md`. |
| 5 | Polish repos: README, architecture diagrams, benchmark tables, reproducible commands. | Portfolio polish. | Artifact-grounded: Can a reviewer understand the artifact in 90 seconds? | Repo cleanup checklist. |
| 6 | Publish one LinkedIn post with a diagram and link to the repo. | Public signal. | Artifact-grounded: Does the post teach one thing and avoid sounding like a course certificate? | LinkedIn post 1. |
| 7 | Apply or reach out to 5 people/projects. | Career conversion. | Synthesis: Which role and artifact are you leading with? | Application tracker with artifact links. |

## Checkpoint Format

For each day, write answers in this format:

```markdown
# Week N Day M Checkpoint

## Type
Source-grounded / Artifact-grounded / Synthesis / Prior experience

## Source or artifact
Link, file path, or "my prior experience".

## Question
...

## My answer
2 to 5 sentences.

## Confidence
High / Medium / Low

## Follow-up
One link or experiment I should revisit.
```

## Take-Home Project Specs

### Project 1: AI Cluster Scheduler Lab

Build a simulator that admits and schedules synthetic AI jobs across a GPU/TPU cluster.

Required features:

- Nodes with CPU, memory, GPU/TPU type, interconnect group, health, and allocated devices.
- Jobs with priority, team, GPU count, duration, preemptible flag, gang size, and checkpoint cost.
- FIFO, fair-share, priority/preemption, and gang scheduling modes.
- Metrics: utilization, pending time, preemption count, failed placements, recovered jobs.
- README section mapping features to Kubernetes Device Plugins, Kueue, Volcano, Ray, and Slurm.

LinkedIn angle: "I built a small AI cluster scheduler simulator to understand why 100 percent allocation is not the same as useful utilization."

### Project 2: Distributed Training Reliability Lab

Build a tiny training job that can run single-process, DDP, and optionally FSDP.

Required features:

- One tiny transformer or MLP with deterministic synthetic data.
- CLI flags for world size, strategy, checkpoint interval, and fail-at-step.
- Checkpoint/resume for model, optimizer, RNG, step, and data position.
- Metrics: step time, tokens/sec, checkpoint time, recovery time, lost work.
- README explaining what changes at 100+ or 1000+ GPUs.

LinkedIn angle: "A tiny training job can still teach the expensive parts: checkpointing, recovery, throughput, and process coordination."

### Project 3: KV Cache Serving Lab

Implement a simulator for memory-aware LLM serving.

Required features:

- PagedAttention-style fixed-size block allocator.
- RadixAttention-style prefix tree cache with LRU eviction.
- Synthetic traces for chat, RAG, and agent loops.
- Metrics: hit rate, allocated blocks, evictions, TTFT proxy, throughput proxy.
- README comparing vLLM and SGLang ideas.

LinkedIn angle: "KV cache management is virtual memory for LLM serving."

### Project 4: Agentic Post-Training Rollout Lab

Build a tiny async rollout and reward harness.

Required features:

- Task queue, rollout worker, reward worker, trainer placeholder.
- Reward functions for math format or code tests.
- Retry/backoff, timeout, and failure categorization.
- Metrics: rollout latency, reward latency, pass rate, retries, queue depth.
- README explaining how this maps to TRL, verl, OpenRLHF, and agentic post-training systems.

LinkedIn angle: "Post-training looks like ML, but the hard parts are distributed systems, queues, sandboxing, and observability."

### Project 5: Kernel Benchmark Lab

Build a small performance benchmark.

Required features:

- Baseline PyTorch implementation.
- CUDA/Triton implementation if hardware allows; otherwise documented kernel code and CPU/GPU PyTorch profiler run.
- Warmup, repeated timing, shape sweep, CSV output.
- Correctness check with tolerance.
- README explaining memory bandwidth, arithmetic intensity, and profiler observations.

LinkedIn angle: "I used a tiny kernel benchmark to learn how memory hierarchy shapes AI performance."

### Project 6: JAX/XLA/Pallas Lab

Build a JAX/Pallas artifact.

Required features:

- One Pallas kernel, such as vector add, tiled matmul, layernorm, or block operation.
- JAXPR and HLO/StableHLO dump where possible.
- Notes on HLO ops, fusion, sharding, and SPMD partitioning.
- TPU notes: what was tested locally and what would need TPU access.
- README mapping this to TPU/JAX/XLA systems expectations.

LinkedIn angle: "I traced a tiny JAX/Pallas program from Python-level code down toward compiler IR to understand TPU systems work."

## Weekly Application Positioning

At the end of each week, update the top of your GitHub README with:

- This week I learned:
- Artifact shipped:
- Production implication:
- Open question:
- AI infra track mapped:

Use this wording style in public:

- Strong: "I built a small simulator to understand scheduling tradeoffs in AI clusters."
- Strong: "I measured checkpoint recovery and throughput in a toy distributed training job."
- Avoid: "I mastered Kubernetes GPU scheduling in a week."
- Avoid: "This is production-ready."

## What To Apply With After 12 Weeks

Cluster / Platform application package:

- Lead with `01-cluster-scheduler`, `02-training-reliability`, and observability/runbooks.
- Resume keywords: GPU/TPU cluster scheduling, fair share, preemption, gang scheduling, checkpoint-aware scheduling, Linux/network debugging, Kueue/Volcano/Ray/Slurm.

Training application package:

- Lead with `02-training-reliability`, `04-post-training-rollouts`, and `03-kv-cache-serving`.
- Resume keywords: FSDP/DDP, TorchTitan, checkpoint/resume, fault recovery, post-training rollouts, reward harness, SGLang/vLLM, distributed observability.

SGLang contributor application package:

- Lead with `03-kv-cache-serving`, `04-post-training-rollouts`, SGLang issue/PR history, and benchmark/repro artifacts.
- Resume keywords: SGLang, LLM serving, RadixAttention, KV cache, continuous batching, structured generation, TTFT, ITL, throughput, goodput, reproducible benchmark, open-source contribution.

TPU Systems application package:

- Lead with `06-jax-xla-pallas`, plus `03-kv-cache-serving`.
- Resume keywords: JAX, XLA, Pallas, StableHLO, SPMD partitioning, sharding, latency/throughput optimization.

Kernel / Compiler / Communication application package:

- Lead with `05-kernel-bench`, `08-collectives` notes if split out, and `06-jax-xla-pallas`.
- Resume keywords: CUDA, GPU memory hierarchy, kernel profiling, NCCL collectives, all-reduce, XLA/HLO, compiler/runtime profiling.

Honest expectation: with 1 hour daily, you can become application-ready for Cluster/Platform and credible for Training in 12 weeks if you ship artifacts. TPU Systems becomes plausible with a strong Pallas/XLA repo. Kernel/Compiler/Communication should be treated as a longer specialization after this plan.
