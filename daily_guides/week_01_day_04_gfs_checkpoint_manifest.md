# Week 1 Day 4 - GFS And Training Checkpoint Manifests

Today should teach one real idea:

GFS is a lesson in metadata design. Large distributed systems can store huge data blocks on many machines, but correctness and recovery depend on small, carefully managed metadata: names, chunk IDs, replica locations, operation logs, leases, checkpoints, checksums, and versions.

## 60-Minute Plan

### 0-5 minutes - Write the objective

Open:

`notes/week_01/day_04_gfs_checkpoint_manifest.md`

Write:

```markdown
Objective: explain how GFS separates metadata from data, why the master matters, how logs/checkpoints support recovery, and what metadata a distributed training checkpoint manifest must store.
```

### 5-15 minutes - Read the official MIT context

Read:

- MIT 6.5840 schedule: https://pdos.csail.mit.edu/6.824/schedule.html
- MIT GFS FAQ: https://pdos.csail.mit.edu/6.824/papers/gfs-faq.txt

Notice:

- MIT places GFS right after MapReduce.
- MapReduce needs a distributed storage substrate for large files, intermediate outputs, and batch-processing data.
- GFS is about a single master, chunkservers, large files, replication, relaxed consistency, and recovery.

Write down:

```markdown
MIT/GFS first impression:
- Why GFS appears after MapReduce:
- What the master owns:
- What chunkservers own:
- Why this matters for AI checkpoint storage:
```

### 15-35 minutes - Read the GFS paper selectively

Read:

- GFS paper: https://pdos.csail.mit.edu/6.824/papers/gfs.pdf

Read these sections only:

- Abstract
- 1 Introduction
- 2.1 Assumptions
- 2.3 Architecture
- 2.4 Single Master
- 2.5 Chunk Size
- 2.6 Metadata
- 2.6.3 Operation Log
- 2.7.2 Implications for Applications
- 3.1 Leases and Mutation Order, skim only

Extract these ideas:

- Component failures are normal at cluster scale.
- GFS stores large files split into fixed-size chunks.
- Chunkservers store chunk data; the master stores metadata.
- Clients ask the master for metadata, then read/write data directly with chunkservers.
- The master keeps namespace, access control, file-to-chunk mapping, and chunk location metadata.
- The operation log is the persistent timeline of metadata changes.
- Master checkpoints speed recovery by avoiding replaying an unbounded log.
- Applications often write self-validating records and use checkpoints so readers avoid incomplete data.
- Leases help choose a primary replica for mutation order.

### 35-45 minutes - Build the GFS concept map

Fill:

`notes/week_01/day_04_gfs_checkpoint_manifest.md`

```markdown
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
```

### 45-55 minutes - Design the checkpoint manifest artifact

Open:

`artifacts/week_01/checkpoint_manifest.json`

Fill it as a design artifact. It does not need to be executable yet. It should answer:

- Which training step is this checkpoint?
- Which model shards exist?
- Which optimizer shards exist?
- Which dataloader position or sample index is resumable?
- Which RNG states are needed?
- Which files are required?
- What checksums prove files are complete?
- What version/schema created this manifest?
- Which distributed ranks/world size produced it?

Then fill this table in the notes file:

```markdown
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
```

### 55-60 minutes - Answer checkpoint questions

Write answers in:

`checkpoints/week_01_day_04.md`

#### A. Source-grounded questions from the GFS paper

1. Why does GFS use a single master?
2. What metadata does the GFS master store?
3. Why does the client talk to the master for metadata but not for file data?
4. Why is the operation log central to GFS recovery?
5. Why does the master create checkpoints?
6. What problem do leases help solve?
7. Why do checksums or self-validating records matter?

#### B. Artifact-grounded questions from your checkpoint manifest

8. What metadata must a training checkpoint store to be resumable?
9. Which fields prevent using an incomplete or corrupted checkpoint?
10. Which GFS idea most influenced your checkpoint manifest design?

## Expected Output

By the end of the hour, you should have:

- `notes/week_01/day_04_gfs_checkpoint_manifest.md`
- `artifacts/week_01/checkpoint_manifest.json`
- `checkpoints/week_01_day_04.md`
- A filled GFS concept map
- A checkpoint manifest design table
- Answers to 7 source-grounded questions and 3 artifact-grounded questions

This is a good Day 4 if you can explain this sentence in your own words:

"The data files are large, but recovery depends on small metadata that says exactly what exists, where it is, what version it is, and whether it is complete."
