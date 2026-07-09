# AGENTS.md

Agent-facing context for this repo lives in [`AGENT.md`](AGENT.md) (build,
test, and lint commands; architecture map; code style) — this file exists
alongside it under the `AGENTS.md`/`CLAUDE.md` filename convention that
agent tooling looks for by default.

This repo is an Elastic-maintained fork of
[`buildkite/agent`](https://github.com/buildkite/agent), re-pointed at
Elastic-specific Buildkite CI queues (see `.buildkite/pipeline.yml`).
`AGENT.md` is shared with upstream — if it goes stale, prefer fixing it
there over duplicating content into this file.
