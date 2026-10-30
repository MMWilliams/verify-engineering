---
name: verify-engineering
description: Require context-grounded engineering practices and runnable verification for software changes and readiness reviews. Use when implementing, fixing, refactoring, or assessing code that needs evidence-based acceptance checks rather than agent-selected tests alone.
---

# Verify Engineering

Treat verification as an evidence obligation. Derive acceptance checks from the task, repository rules, established contracts, and credible failure modes before implementing. Passing tests selected solely to match the new implementation is insufficient.

This skill governs the current task; it does not authorize unrelated cleanup, external mutations, or changes to repository protections. It provides procedural safeguards, not tamper-proof enforcement. Do not claim it configures CI or branch protections.

## Establish the engineering context

Inspect the relevant repository instructions, contribution rules, build manifests, scripts, CI workflows, test configuration, and nearby implementation/tests. Trace changed interfaces to their callers and consumers. Identify applicable architecture constraints, runtime/dependency versions, and external services.

Use that evidence to select engineering practices appropriate to the change: compatibility, error handling, input validation, security boundaries, data integrity, concurrency, resource use, accessibility, performance, and maintainability where relevant. Do not impose every category on every task. Explain material exclusions when a risk is plausible, rather than silently omitting it.

Repository policies and existing mandatory gates are the minimum. Add checks for requirements or failure modes they do not exercise. Do not substitute a generic checklist for repository discovery. If evidence conflicts, identify the conflict; use instruction precedence and resolve material ambiguity before implementing dependent behavior.

## Define verification before implementation

Create a compact verification matrix in the working notes or response before changing behavior. Use an existing repository verification-plan format if provided; otherwise use:

| Requirement or material risk | Source | Runnable check | Explicit pass criterion | Result/evidence |
| --- | --- | --- | --- | --- |

Every material acceptance requirement and identified risk must map to a check. Record:

- A concrete source: task acceptance criterion, policy path, specification section, existing public contract, established baseline, or named engineering invariant with its rationale. Distinguish inferred risks from explicit requirements.
- An executable command, working directory, necessary environment or fixtures, and the behavior it exercises. A prose instruction to "test thoroughly" does not qualify.
- A meaningful expected outcome established independently of the implementation. Use specification examples, invariants, trusted reference behavior, pre-change baselines, or reproducible reported failures. Do not compute expected values by repeating the implementation under test or snapshot its output without review.
- An initial status of pending, then actual evidence. Separate manual review obligations from runnable checks; neither silently substitutes for the other.

Keep the plan proportional. A small change may need a few rows and existing checks only; do not invent tests that mirror implementation or add an entire testing framework without need. For a review of completed work, establish the matrix before judging readiness and identify any missing pre-change evidence honestly.

Use executable checks for requirements that can reasonably be checked automatically. If a criterion genuinely requires human judgment, state the concrete review method and its limits. If an essential requirement is unknown, request only the missing information and continue independent work.

Update the matrix when discovery changes scope, with the source and reason. Do not remove a failed criterion merely to make the final report pass.

## Implement and exercise the actual behavior

Reuse the project's supported tools and execution environments. Inspect existing tests for relevance and execution conditions, not just their names. For a bug fix, reproduce the failure or demonstrate that the regression check fails against the original behavior when feasible. Explain if a baseline run is unavailable.

Choose evidence that can detect plausible incorrect implementations. Include relevant boundaries, invalid inputs, failure paths, and compatibility effects as dictated by the matrix. Exercise real integrations when the contract depends on a database, service, browser, filesystem, or protocol. Mocks can supplement such evidence but do not establish real integration correctness.

Run the applicable repository gates and planned behavioral checks on the final state. This can include build, static analysis, type checks, unit/integration/end-to-end tests, migration verification, security checks, accessibility checks, or measurements against an established performance baseline. Use the subset justified by context and mandatory policy; do not invent thresholds or declare a best practice satisfied solely because a tool exits successfully.

Record exact commands, relevant environment, exit codes, and useful output summaries. Inspect test discovery, executed/skipped counts, filters, warnings, and generated artifacts where applicable. Exit zero with no relevant tests executed is not verification. An all-skipped suite supplies no behavioral evidence; a partial skip must be mapped to requirements it leaves uncovered. Coverage numbers alone do not prove assertions are meaningful.

After a failure, diagnose and fix the cause within scope, then rerun the affected checks. After subsequent edits, rerun checks affected by those edits. Reuse prior results only when the checked code, configuration, dependencies, fixtures, and environment remain applicable; identify evidence obtained on another revision or environment.

## Preserve verification integrity

- Do not weaken assertions, delete coverage, skip failing tests, relax thresholds, disable gates, or alter discovery just to get a pass.
- Test, fixture, snapshot, and CI changes are legitimate only when independently supported by a changed requirement, documented contract, or demonstrated test defect. Explain that source and preserve the original intended protection. An unexpected result is not itself a reason to update the expectation.
- Do not silently replace unavailable integration checks with mocks, treat a blocked check as passed, or invent execution evidence.
- Do not bypass repository requirements or install unrelated infrastructure just to finish. Complete available checks and report the remaining gap precisely.
- Distinguish pre-existing or unrelated failures using a baseline when possible. They may explain a failure but do not turn the required gate green.

## Close with evidence

Report the changed behavior, checks actually run with outcomes, and material limitations. Keep routine output concise while retaining enough command and result detail to reproduce verification. Use an existing report location if the repository requires one; otherwise a final response is enough.

Give the task one of these conclusions:

- **Verified:** All applicable required gates and material acceptance checks passed on the relevant final state, with actual execution and no unresolved essential evidence gaps.
- **Partially verified:** Some checks passed, but required checks are blocked, skipped, unexecuted, or otherwise insufficient. State each uncovered requirement, the reason, and the exact next check needed.
- **Failed verification:** A required gate or acceptance check failed. Identify the failure and its scope, including any demonstrated pre-existing failure.

Use failed verification if a failure and missing evidence both exist, and disclose both. Completion of implementation is distinct from verified acceptance. Do not call the task verified or ready for release while essential evidence is missing; scope narrower claims to the checks that actually passed.
