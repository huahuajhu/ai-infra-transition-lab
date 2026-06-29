# Week 1 Day 4 Checkpoint

## Status

Not started.

## Sources

- MIT 6.5840 schedule: https://pdos.csail.mit.edu/6.824/schedule.html
- MIT GFS FAQ: https://pdos.csail.mit.edu/6.824/papers/gfs-faq.txt
- GFS paper: https://pdos.csail.mit.edu/6.824/papers/gfs.pdf

## Type

Source-grounded + artifact-grounded

## A. Source-Grounded Questions From The GFS Paper

### 1. Why does GFS use a single master?

My answer:

Confidence:

### 2. What metadata does the GFS master store?

My answer:

Confidence:

### 3. Why does the client talk to the master for metadata but not for file data?

My answer:

Confidence:

### 4. Why is the operation log central to GFS recovery?

My answer:

Confidence:

### 5. Why does the master create checkpoints?

My answer:

Confidence:

### 6. What problem do leases help solve?

My answer:

Confidence:

### 7. Why do checksums or self-validating records matter?

My answer:

Confidence:

## B. Artifact-Grounded Questions From The Checkpoint Manifest

### 8. What metadata must a training checkpoint store to be resumable?

My answer:

Confidence:

### 9. Which fields prevent using an incomplete or corrupted checkpoint?

My answer:

Confidence:

### 10. Which GFS idea most influenced your checkpoint manifest design?

My answer:

Confidence:

## Follow-Up

- Revisit this during Week 4 when implementing checkpoint/resume in the distributed training reliability lab.
