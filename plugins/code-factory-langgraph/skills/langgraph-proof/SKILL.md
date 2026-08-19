---
name: langgraph-proof
description: Use when building, reviewing, or debugging a LangGraph flow that must prove a resumed run preserved its recorded semantic transitions and side-effect discipline.
---

# Code Factory LangGraph Proof

Use Code Factory as a local proof layer around a team-owned LangGraph test
harness. It is not a graph runtime, checkpoint store, repair agent, or release
authority.

## Start with the boundary

Before relying on the MCP server, check that the current workspace has the
Code Factory CLI and inspect its stated local boundary:

```bash
factory --version
factory mcp status --root .
```

If the CLI is missing, explain that the user must install
`factoryline-code-factory>=0.39.0` in the environment that will host the local
MCP process. Do not install Python packages, change a client configuration, or
start a server without the user's approval.

## What to prove

For a LangGraph flow with a durable checkpoint or interruption path, ask for:

1. A team-owned reference harness run.
2. A separately captured resumed or interrupted run.
3. Two sealed, workspace-relative transition lineages. The recorder retains
   SHA-256 facts about state and side-effect identifiers, not raw state,
   prompts, or secrets.

Compare existing lineages without writing a file:

```bash
factory langgraph replay-verify \
  --root . \
  --reference .factory/langgraph/reference.json \
  --resumed .factory/langgraph/resumed.json \
  --json
```

Only add `--out .factory/langgraph/assurance.json` after the user explicitly
approves writing a local assurance receipt.

## Interpret the result precisely

- `LANGGRAPH_RESUME_PARITY_VERIFIED` means the supplied sealed lineages match
  semantically and the deterministic analysis found no supported anomaly.
- `LANGGRAPH_REPLAY_DIVERGENCE` means the supplied evidence differs or exposes
  duplicate completed effects, stale reads/writes, or unsafe parallel writes.
  Present the incident capsule and recovery cone for human review.
- `LANGGRAPH_INPUT_REJECTED` means the comparison was rejected before a
  receipt was written; fix the supplied inputs rather than guessing.

Never claim that a parity receipt proves production resilience, complete
instrumentation, external idempotency, savings, quality, or correctness beyond
the supplied lineages.

## MCP use

`factory.langgraph_assurance` is read-only. It may compare two existing
workspace-relative receipts; it cannot invoke a graph, mutate checkpoints,
replay effects, write a receipt, approve a repair, merge, deploy, publish,
send a message, or access credentials.

If a divergence needs code changes, prepare a narrow repair proposal and tests
for a human to approve. Do not authorize or execute repairs from the incident
capsule.
