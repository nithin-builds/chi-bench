# CareProof Agent

CareProof is a reliability-focused configuration of the official χ-Bench
OpenAI Agents harness. It is designed for strict binary workflow evaluation:
one missing prerequisite, unverified mutation, or unsupported claim can make a
task fail.

## Design

- **Scope lock:** derives and obeys the allowed tool namespaces for each task.
- **Evidence ledger:** separates sourced facts from missing or conflicting data.
- **Dependency gate:** completes prerequisites before consequential mutations.
- **Safe recovery:** retries only after interpreting structured errors and avoids
  duplicate successful mutations.
- **Completion proof:** reads state back after changes and audits the terminal
  workflow state before stopping.
- **Conversation safety:** requires performed consent and disclosure steps rather
  than inferring them from cooperation.

The protocol contains no task answers or protected handbook content. It relies
on the authorized handbook mounted by the official evaluator at runtime.

## Validate

```bash
uv sync --extra dev
uv run pytest tests/unit/test_careproof_prompt.py
uv run cb submission validate \
  -f configs/submissions/careproof-gpt-5-6-sol.yaml \
  --skip-preflight
```

Full benchmark execution additionally requires approved handbook access, the
pinned public dataset, environment credentials, and either Modal or the local
Docker image as documented by χ-Bench. Do not commit `.env`, API keys, a Hugging
Face token, or handbook files.

## Honest status

The harness integration and deterministic prompt checks can be verified without
the gated handbook. Public pass@1 and pass³ must not be claimed until the
official verifier has produced those results from authorized runs.
