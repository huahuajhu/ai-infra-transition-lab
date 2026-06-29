# SGLang Six-Month Contributor Track

Objective: become a trusted recurring SGLang contributor in six months.

This is more controllable than saying "become maintainer in six months." Maintainer status depends on project needs, maintainer trust, review bandwidth, and governance. The concrete target is:

- 8 to 12 merged PRs or high-quality accepted contributions.
- At least 2 code PRs with tests, not only docs.
- At least 2 reproducible benchmark, profiling, or bug-report artifacts.
- Helpful issue triage in one subsystem.
- Enough subsystem familiarity that maintainers recognize your work.

Primary repo: https://github.com/sgl-project/sglang

Primary docs:

- SGLang docs: https://docs.sglang.io/
- Contribution guide: https://docs.sglang.io/docs/developer_guide/contribution_guide
- Developer overview: https://docs.sglang.io/docs/developer_guide/overview
- Benchmark and profiling guide: https://docs.sglang.io/docs/developer_guide/benchmark_and_profiling
- Serving benchmark guide: https://docs.sglang.io/docs/developer_guide/bench_serving
- SGLang paper/blog: https://www.lmsys.org/blog/2024-01-17-sglang/

## Why SGLang

SGLang is the best primary target for this plan because it connects several strengths you already have:

- Production LLM/RAG and agent service experience.
- DevOps/platform instincts around reliability, observability, testing, and reproducibility.
- Interest in inference runtime internals, KV cache behavior, batching, and serving metrics.
- Future post-training interest, where generation throughput and rollout serving matter.

Use vLLM as an important comparison source, but do not split contribution energy across both repos at first.

## Target Subsystem

Start with serving/runtime observability and KV-cache-adjacent behavior.

Good initial areas:

- Docs that explain serving behavior, benchmark usage, or operational tradeoffs.
- Unit tests for runtime behavior.
- Repro scripts for serving bugs or benchmark regressions.
- Metrics, logging, configuration clarity, or error-message improvements.
- Small fixes around request scheduling, caching behavior, or benchmark tooling after you understand the path.

Avoid as first PRs:

- Large kernel rewrites.
- Major scheduler redesigns.
- Broad refactors.
- New feature proposals without maintainer signal.
- Changes that require expensive hardware you cannot test.

## Weekly Time Budget

Keep the 1-hour daily study limit.

- Monday to Friday: 10 minutes SGLang watch, 50 minutes normal study.
- One weekend day: 60 minutes SGLang contribution work.
- If a course day is heavy, skip the SGLang watch that day and recover on the weekly SGLang session.

The goal is steady presence, not heroic bursts.

## First 14 SGLang Sessions

### Session 1 - Contribution Rules

Read:

- https://docs.sglang.io/docs/developer_guide/contribution_guide

Write:

- `open_source/sglang_repo_map.md`

Capture:

- How to install from source.
- How formatting works.
- How unit tests are organized.
- What accuracy tests and speed benchmarks are for.
- What maintainers expect before review.
- How CI is triggered.
- What the newcomer tips recommend.

Checkpoint:

What does a good SGLang PR need besides code?

### Session 2 - Repo Shape

Read:

- SGLang GitHub README.
- Top-level directories in the repo.
- Developer overview.

Write:

- Top-level directory map.
- "I think this directory owns..." for each important path.
- Three directories that seem closest to your skills.

Checkpoint:

Which part of SGLang feels closest to your current production LLM service experience?

### Session 3 - Runtime User Path

Read:

- Docs quickstart.
- One basic serving example.

Trace:

- User request enters API/server.
- Request becomes runtime work.
- Runtime schedules model execution.
- Output tokens stream back.

Checkpoint:

What is the difference between SGLang as a programming interface and SGLang as a serving runtime?

### Session 4 - Recent PR Reading

Read:

- Three recent merged PRs in SGLang.

Write:

- What changed.
- What tests were added.
- What reviewer comments appeared.
- What you would have needed to know to make that PR.

Checkpoint:

What does a small accepted SGLang contribution look like?

### Session 5 - Issue Triage

Read:

- Five open issues.

Create:

- `open_source/sglang_issue_shortlist.md`

For each issue:

- Link.
- Problem type: bug, docs, test, benchmark, feature, question.
- Reproducible locally: yes/no/unknown.
- Hardware needed.
- Risk level.
- Possible first helpful action.

Checkpoint:

Which issue is small, reproducible, useful, and not blocked by unavailable hardware?

### Session 6 - Tests Map

Read:

- Contribution guide section on tests.
- Test directories that map to one runtime/source directory.

Write:

- Test naming convention.
- How to run one small test.
- What fixture or mock style appears.

Checkpoint:

Where would you add a test for a runtime bug?

### Session 7 - Benchmark Map

Read:

- Benchmark and profiling guide.
- Serving benchmark guide.

Write:

- What benchmark inputs matter.
- What metrics matter.
- Which benchmark you can run locally.
- Which benchmark needs GPU/cloud.

Checkpoint:

What would make a benchmark result credible to maintainers?

### Session 8 - Docs PR Candidate

Find:

- One docs paragraph, command, error message, or concept explanation that could be clearer.

Draft:

- Problem.
- Proposed wording.
- Why it helps users.
- Link to source or behavior.

Checkpoint:

Is this improvement small enough to review quickly?

### Session 9 - Repro Script Candidate

Find:

- One issue where a minimal repro would help.

Draft:

- Environment.
- Install command.
- Minimal command/script.
- Expected behavior.
- Actual behavior.
- Logs.

Checkpoint:

Can another contributor reproduce this without guessing?

### Session 10 - First Local Patch

Make:

- One local docs/test/repro patch.

Check:

- Formatting.
- Targeted test.
- Clear commit message.
- Small diff.

Checkpoint:

Would a maintainer understand the purpose in 60 seconds?

### Session 11 - First PR or Issue

Publish one of:

- Small docs PR.
- Test PR.
- Repro issue.
- Benchmark issue.

Write:

- Link.
- What you learned.
- What feedback you got.

Checkpoint:

What changed after maintainer feedback?

### Session 12 - Subsystem Choice

Choose one primary subsystem for Months 2 to 6.

Recommended order:

1. Runtime/serving observability.
2. Benchmark/profiling tooling.
3. KV-cache or prefix-cache behavior.
4. Request scheduling behavior.

Checkpoint:

Which subsystem has enough issues, tests, and docs for repeated contribution?

### Session 13 - Code Walk

Pick one function or class in the subsystem.

Write:

- Inputs.
- Outputs.
- Side effects.
- Error cases.
- Tests.
- Metrics/logs.

Checkpoint:

What invariant must this code preserve?

### Session 14 - Contribution Plan

Write a four-week contribution queue:

- One docs/test cleanup.
- One reproducible issue or benchmark artifact.
- One small code fix.
- One deeper code-reading note.

Checkpoint:

What is the next smallest useful contribution?

## Six-Month Ladder

### Month 1 - Learn The Project And Earn First Contact

Goal:

- Understand contribution rules.
- Map the repo.
- Read issues and merged PRs.
- Make one small contribution or one high-quality issue.

Output:

- `open_source/sglang_repo_map.md`
- `open_source/sglang_issue_shortlist.md`
- One docs/test/repro contribution attempt.

Success metric:

You can explain how to make, test, and submit a small SGLang change.

### Month 2 - Become Useful In Triage

Goal:

- Help clarify issues.
- Reproduce one bug or benchmark behavior.
- Make one docs/test PR.

Output:

- Repro script or benchmark note.
- One accepted or actively reviewed PR.

Success metric:

Your comments reduce maintainer work by adding evidence, not opinions.

### Month 3 - First Real Code Fix

Goal:

- Make one small runtime, benchmark, or test-related code fix.
- Include a targeted test or benchmark evidence.

Output:

- One code PR with test.
- One writeup explaining the subsystem path touched by the PR.

Success metric:

You can trace a user-visible serving behavior into the code path you changed.

### Month 4 - Own A Narrow Subsystem Slice

Goal:

- Stay in one subsystem.
- Improve docs, tests, and bug handling around the same area.

Output:

- Two additional PRs or strong issue/benchmark artifacts.
- A local note titled "SGLang subsystem invariants."

Success metric:

You can predict what maintainers will ask about a change before they ask it.

### Month 5 - Contribute With Performance Awareness

Goal:

- Add or improve benchmark coverage.
- Explain latency/throughput tradeoffs clearly.

Output:

- Benchmark issue/PR or profiling note.
- One public portfolio note connecting your KV cache lab to SGLang behavior.

Success metric:

Your contribution includes enough measurement detail to be useful.

### Month 6 - Trusted Contributor Packet

Goal:

- Package your contribution history.
- Ask maintainers where help is most useful.
- Continue contributing in the same subsystem.

Output:

- Contribution log with PR/issue links.
- "What I learned contributing to SGLang" writeup.
- Resume bullet and interview story.

Success metric:

You have visible repeated contribution behavior, not a one-off PR.

## Contribution Log Template

Use this table in `open_source/sglang_contribution_log.md`.

| Date | Link | Type | Area | What I contributed | Tests/evidence | Status | Maintainer feedback | Next step |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| YYYY-MM-DD |  | docs/test/code/issue/benchmark |  |  |  | planned/open/merged/closed |  |  |

## Public Positioning

Strong:

- "I am building toward recurring contribution in SGLang by focusing on serving-runtime behavior, tests, and reproducible benchmarks."
- "I wrote a KV-cache simulator to understand the systems ideas behind SGLang-style serving."
- "My goal is to reduce maintainer load with small, well-tested, reproducible contributions."

Avoid:

- "I will become an SGLang maintainer in six months."
- "I mastered SGLang."
- "This benchmark proves production performance."

## Resume Bullet Shape

Draft after the first accepted contribution:

- Contributed to SGLang by improving [area], adding [test/benchmark/repro], and documenting [behavior], building practical depth in LLM serving runtime internals, KV cache behavior, and reproducible performance debugging.
