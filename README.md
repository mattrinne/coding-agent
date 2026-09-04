# coding-agent

A locally-run coding agent, built from scratch to understand how systems like Claude Code work
internally — using a local Ollama model instead of a paid API. See [docs/SPEC.md](docs/SPEC.md)
for the full project spec.

## Status

Early scaffolding — no working CLI yet. See the project's GitHub issues for the current
milestone.

## Requirements

- Node.js >= 20
- npm

## Setup

```bash
npm install
```

## Scripts

```bash
npm run build  # compile TypeScript to dist/
npm test       # run the test suite (Vitest)
npm run lint   # lint with ESLint
npm run format # format with Prettier
```
