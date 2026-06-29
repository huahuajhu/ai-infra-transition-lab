# Week 1 Day 1 Checkpoint

## Status
Completed source-grounded questions from "First Steps: Training on One GPU".

## Source
Hugging Face Ultra-Scale Playbook: https://nanotron-ultrascale-playbook.static.hf.space/index.html#first_steps:_training_on_one_gpu

## Type
Source-grounded

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

## Follow-up

Continue with the synthesis questions in `notes/week_01/day_01_stack_map.md` after reviewing the CS336 field map and AI infrastructure stack map.
