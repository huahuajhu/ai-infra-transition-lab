# Week 1 Day 4 - GFS And Training Checkpoint Manifests

Objective: explain how GFS separates metadata from data, why the master matters, how logs/checkpoints support recovery, and what metadata a distributed training checkpoint manifest must store.

## Sources

- MIT 6.5840 schedule: https://pdos.csail.mit.edu/6.824/schedule.html
- MIT GFS FAQ: https://pdos.csail.mit.edu/6.824/papers/gfs-faq.txt
- GFS paper: https://pdos.csail.mit.edu/6.824/papers/gfs.pdf

## Reading Notes

MIT/GFS first impression:

- Why GFS appears after MapReduce:
- What the master owns:
- What chunkservers own:
- Why this matters for AI checkpoint storage:

GFS paper notes:

- Component failures:
- Large files and chunks:
- Master:
- Chunkservers:
- Metadata:
- Operation log:
- Master checkpoint:
- Lease:
- Checksums/self-validating records:

## GFS Concept Map

| GFS concept | What the paper means | Training checkpoint analogy | Confidence |
| --- | --- | --- | --- |
| Large file |  |  |  |
| Chunk |  |  |  |
| Chunkserver |  |  |  |
| Master |  |  |  |
| Metadata |  |  |  |
| Operation log |  |  |  |
| Master checkpoint |  |  |  |
| Replica |  |  |  |
| Lease |  |  |  |
| Checksum/self-validating record |  |  |  |

## Checkpoint Manifest Design

| Manifest field | Why recovery needs it | What can go wrong if missing |
| --- | --- | --- |
| checkpoint_id |  |  |
| global_step |  |  |
| model_shards |  |  |
| optimizer_shards |  |  |
| scheduler_state |  |  |
| rng_state |  |  |
| dataloader_state |  |  |
| world_size_and_ranks |  |  |
| file_checksums |  |  |
| schema_version |  |  |

## Recovery Walkthrough

Use the manifest to answer these in order:

1. Which checkpoint should the job load?
2. Are all required files present?
3. Do checksums match?
4. Do model shards, optimizer shards, ranks, and world size match the resume configuration?
5. Which global step, RNG state, scheduler state, and dataloader position should resume?

## Open Questions

- 
