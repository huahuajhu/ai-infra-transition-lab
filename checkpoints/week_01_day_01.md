# Week 1 Day 1 Checkpoint

## Status
Completed source-grounded questions from "First Steps: Training on One GPU" and first-pass synthesis questions from the Day 1 stack map.

## Source
Hugging Face Ultra-Scale Playbook: https://nanotron-ultrascale-playbook.static.hf.space/index.html#first_steps:_training_on_one_gpu

## Type
Source-grounded + synthesis

## Questions And Answers

### 1. Where is batch size represented in the forward/backward training picture?

Batch size is not drawn explicitly. It is hidden inside the forward and backward arrows as the number of examples processed together in one training step or micro-batch.

Confidence: High

### 2. What is activation recomputation, in plain English?

Activation recomputation saves memory by not storing every intermediate activation from the forward pass. Instead, training keeps selected checkpoint activations and reruns parts of the forward computation during backward when those intermediate values are needed again.

Confidence: High

### 3. What is the difference between full and selective activation recomputation?

Full recomputation reruns whole chunks or blocks during backward. Selective recomputation keeps some activations and only recomputes the parts that are expensive in memory, trading less extra compute for a smaller memory saving than full recomputation.

Confidence: High

### 4. If full recomputation discards intermediate activations, what does it still keep?

It does not discard everything. It keeps boundary checkpoint activations, such as the input to a block, and uses those saved boundary values to recreate internal activations later during backward.

Confidence: High

### 5. What is gradient accumulation, and why does it help when a large batch does not fit in memory?

Gradient accumulation splits a large batch into smaller micro-batches. The system runs forward and backward repeatedly, accumulates gradients across those micro-batches, and performs one optimizer step after the accumulated gradients represent the intended larger batch.

Confidence: High

## Synthesis Questions And Answers

These answers are not directly from the Ultra-Scale reading alone. They are first-pass synthesis answers from the CS336 field map and the AI infrastructure stack map.

### 6. What is the difference between a training runtime and a cluster scheduler?

A training runtime owns what happens inside the training job: the forward pass, backward pass, optimizer step, distributed communication, memory strategy, checkpoint writing, and resume logic. A cluster scheduler owns where and when the job runs: GPU/node allocation, placement, quotas, priority, preemption, and gang scheduling.

First-pass summary: the scheduler gives the job resources; the training runtime uses those resources correctly and efficiently.

Confidence: Medium

### 7. What is the difference between an inference runtime and a model API?

A model API is the user-facing service contract: HTTP/gRPC endpoint, request schema, authentication, routing, model selection, streaming response shape, and application logic. An inference runtime is the engine behind that API that actually runs generation efficiently: batching requests, managing the KV cache, scheduling prefill/decode work, using tensor parallelism, controlling GPU memory, and optimizing latency/throughput.

First-pass summary: the API answers "how does a caller ask for a response?" The runtime answers "how do we produce tokens efficiently on accelerators?"

Confidence: Medium

### 8. Why does communication overhead keep accelerators idle?

In distributed training or serving, each accelerator often has only part of the work or part of the model state. Devices must exchange tensors through collectives such as all-reduce, all-gather, reduce-scatter, or pipeline sends/receives. If one GPU finishes compute and then waits for data from another GPU or another node, its compute units sit idle.

First-pass summary: adding more GPUs only helps when communication is small enough, well placed on the topology, or overlapped with useful compute.

Confidence: Medium

### 9. Which layer of the stack would own checkpoint/restart after a worker failure?

This is cross-layer, but the training runtime owns the correctness of checkpoint and restart. It must save and reload model parameters, optimizer state, scheduler state, RNG state, dataloader position, and distributed shard metadata. The cluster scheduler owns restarting or rescheduling the failed worker/job onto resources. Observability/reliability owns detection, alerts, dashboards, and runbooks.

First-pass summary: training runtime owns the state; scheduler owns replacement resources; reliability tooling owns visibility and response.

Confidence: Medium

### 10. Which two stack layers are closest to your current experience?

The closest two are cluster scheduler and observability/reliability. Your DevOps/platform background maps directly to Kubernetes, Kubeflow, Docker, Helm, ArgoCD, AWS infrastructure, CI/CD, production operations, monitoring, logging, and runbooks.

The next closest layers are inference runtime and data pipeline because of your production LLM/RAG/API work and traditional data science/data engineering experience. The biggest stretch layers are kernel/performance, compiler/runtime, and hardware/network.

Confidence: Medium

## Follow-up

Revisit the synthesis answers after Week 2, Week 4, Week 5, and Week 8 as the training, inference, scheduler, and observability parts of the stack become more concrete.
