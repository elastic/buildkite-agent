# Elastic fork guidance

## Purpose and trust boundary

This is Elastic's fork of [`buildkite/agent`](https://github.com/buildkite/agent).
It is not maintained as an independent agent distribution and currently
publishes no releases of its own.

The fork's `main` branch is an operational trust boundary, not a passive mirror.
Elastic's [Gobld Linux VM bootstrap](https://github.com/elastic/gobld/blob/main/providers/linux-startup.sh)
and [Windows CI agent images](https://github.com/elastic/ci-agent-images/tree/main/vm-images)
download `install.sh` or `install.ps1` from this branch. The installers then
resolve and download official Buildkite agent release artifacts; callers can
pin the binary version independently. This indirection keeps executable
installer code consumed by Elastic infrastructure under Elastic ownership.

## Upstream synchronization

- Do not sync this fork from upstream as part of an unrelated change.
- Treat an upstream sync as an operational change. Review changes to
  `install.sh` and `install.ps1`, then validate the affected agent bootstrap and
  image-building paths before updating `main`.
- Keep upstream-owned agent instructions in `AGENTS.md` and Elastic-specific
  guidance in this file. When upstream changes `AGENTS.md`, preserve only its
  single pointer to this file as the Elastic-owned addition.
- Prefer contributing generally useful compatibility fixes upstream after they
  have been validated in Elastic's environments.

## AI attribution

For every AI tool that materially contributes to code, tests, documentation,
configuration, or the substance of a change:

- Resolve the tool's runtime identity and add one unformatted trailer to the
  commit message. Use the exact model or agent slug and reasoning effort whenever
  exposed; omit unavailable components rather than guessing:

  ```text
  Assisted-by: <tool name> (<most specific verified runtime identity>)
  ```

- Repeat the same trailer in the pull-request description.
- Preserve the spelling and specificity of exposed runtime values; do not
  shorten a specific model slug to a broader model family.
- Preserve valid tool-native attribution, such as
  `Made with [Cursor](https://cursor.com)` or a genuine `Co-authored-by`
  trailer, in addition to `Assisted-by`.
- Never invent a bot identity, model name, agent identifier, or email address.
- Keep trailers on their own lines without bullets, Markdown emphasis, or
  surrounding underscores.
- Keep the human author or committer accountable for understanding and
  verifying the change.

For a squash merge, verify that the final squash commit message contains every
attribution trailer. GitHub may populate that message from the pull-request
description, commit information, or only the pull-request title depending on
repository settings, so putting attribution in the PR description improves
preservation but does not guarantee it.

When preparing a commit or pull request, offer to create it with the correct
attribution. If the user will create it manually, show the exact trailers to
copy into both places.
