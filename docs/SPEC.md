# Personal Coding Agent

A locally-run coding agent, built from scratch to understand how systems like Claude Code work internally — using a local Ollama model instead of a paid API.

## Problem & Motivation

Understanding how coding agents work (agent loops, tool use, context management) is best learned by building one, not just reading about one. Budget constraints rule out paid model APIs, so inference runs locally via Ollama.

## Users / Stakeholders

Solo project — built and used by you, for your own coding tasks and learning.

## Goals & Success Criteria

- The agent can complete real, small coding tasks end-to-end (e.g. "add a function," "fix this bug," "write a test") against your own codebases.
- You come away able to explain how the agent loop, tool-calling, and context management work.
- Local inference runs comfortably alongside your other work on the Mac (M3 Max, 36GB) — it shouldn't hog memory/CPU.

## Scope

**In scope (v1):**
- CLI interface first (single-shot / REPL), built in TypeScript/Node.js
- Core tools: read / write / edit files, search the codebase (grep/glob-style)
- Multi-turn conversation memory within a session, so follow-up instructions retain context
- Confirmation prompts before risky actions (file writes) — no silent autonomous edits
- Local inference via Ollama, run in Docker
- Model: not finalized — target a tool-calling-capable model sized to leave headroom on a 36GB machine (e.g. Qwen2.5-Coder or Llama 3.1 in the 7B–14B range, quantized); exact choice is an open question to validate by testing

**Out of scope (for now):**
- Shell command execution (running tests/builds/git) — deliberately deferred to a later phase
- TUI — planned as a future iteration once the CLI version works
- Paid/cloud model fallback
- Multi-user or team features
- Large-scale/multi-repo refactors

## Key User Flows / Features

1. Start the agent CLI pointed at a project directory.
2. Give it a natural-language task.
3. Agent loop: call the model → model requests a tool (read/search/write) → risky actions require your confirmation → tool executes → result feeds back to the model → repeat until the task is done or the model reports completion.
4. Continue the conversation with follow-ups ("now add a test for that") without restating context.
5. Interface evolves from CLI to a richer TUI in a later iteration.

## Constraints & Assumptions

- Inference runs locally via Ollama in Docker on an M3 Max / 36GB Mac; the setup should avoid consuming all available memory/CPU, likely via a smaller quantized model and/or Docker resource limits.
- No paid model APIs.
- No fixed deadline — side-project pace.

## Open Questions

- Which specific Ollama model + quantization to standardize on (needs hands-on testing for speed/quality/memory tradeoffs on this hardware).
- How to structure the confirmation UX in CLI mode before a TUI exists (simple y/n per action?).
- Should session/conversation history persist to disk between runs, or reset each time the CLI starts?
- What Docker resource limits (memory/CPU caps) to set for the Ollama container.
