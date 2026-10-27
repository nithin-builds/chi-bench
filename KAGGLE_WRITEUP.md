# CareProof Agent: Verified-State Control for Reliable Healthcare Workflows

**Team:** nithin-builds  
**Author:** N Nithin Kumar  
**Model:** `openai/gpt-5.6-sol` through the official OpenAI Agents harness  
**Tracks:** Provider Prior Authorization, Payer Utilization Management, Care Management

## Summary

CareProof Agent is a reliability-focused configuration of the official χ-Bench
agent runtime. It targets the benchmark's strict binary scoring rule: a task
passes only when every required non-N/A check succeeds. The design therefore
optimizes for verified workflow completion rather than persuasive narration.

## Method

CareProof adds a nine-step control protocol to the official OpenAI Agents
harness:

1. Lock the task scope, allowed namespaces, target case, terminal objective,
   and prohibitions before acting.
2. Read the authorized handbook index and task tool reference before any
   consequential mutation.
3. Maintain an evidence ledger that separates sourced facts from missing or
   conflicting information.
4. Inspect existing state and tool schemas before creating or changing data.
5. Execute prerequisites in dependency order and avoid duplicate mutations.
6. Treat consent, disclosure, teach-back, refusal, and escalation as performed
   conversational actions, never inferred facts.
7. Verify state after each consequential mutation.
8. Continue until the requested terminal state is reached and proved.
9. Return only a short factual completion report.

The protocol is domain-general: it contains no public-task answers, hidden
expectations, or protected handbook content. The authorized handbook remains a
runtime dependency mounted by the official evaluator.

## Why this should generalize

Public tasks vary clinically, but many failures share operational causes:
out-of-scope tool use, skipped prerequisites, unsupported evidence, premature
stopping, duplicate mutations, and unverified final state. CareProof encodes
controls for those failure classes without specializing to task identifiers or
expected answers, which is important for the unreleased private set.

## Reproducibility

- Runtime: official χ-Bench repository and lock file
- Dataset pin: `chi-bench-v1.0.0`
- Harness: `openai-agents`
- Agent model: `openai/gpt-5.6-sol`
- Attempts: one per public task; three private attempts are organizer-run
- Configuration: `configs/submissions/careproof-gpt-5-6-sol.yaml`
- Prompt checks: `tests/unit/test_careproof_prompt.py`

The complete unit suite passes with 264 tests and 6 environment-dependent
skips. The submission schema also validates. These checks establish integration
correctness, not benchmark quality.

## Results

No public pass@1 or pass^3 score is claimed in this writeup. Official task
execution requires approved access to the gated Managed-Care Operations
Handbook and the required model/judge credentials. Results will be reported
only from unmodified official verifier outputs.

## Limitations and safeguards

- LLM behavior remains nondeterministic and can still miss workflow details.
- The protocol adds reasoning overhead and may increase latency or tool calls.
- Correctness depends on the authorized handbook, model availability, and
  simulator/tool contracts.
- CareProof is a research submission operating on synthetic χ-Bench data. It
  is not a medical device and must not be used for real patient decisions.
- No credentials, real patient data, protected handbook text, or private task
  material are included in the repository or submission package.

## Links

- Source fork: https://github.com/nithin-builds/chi-bench
- Upstream χ-Bench: https://github.com/actava-ai/chi-bench
- Author portfolio: https://github.com/nithin-builds

