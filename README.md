# mise-github-action-debug

Reproduction for

## Context

Using `mise` + `uv` in GitHub workflows with automatic Python virtualenv
activation doesn't work. Running `python` causes the workflow hangs and memory
leak.

## Current behavior

The step `python --version` in `.github/workflows/mise.yaml` hangs.

## Expected behavior

`mise` automatically activates `uv` virtualenv without any issues.
