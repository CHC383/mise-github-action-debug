# mise-github-action-debug

Reproduction for https://github.com/jdx/mise/discussions/5665

## Context

Using `mise` + `uv` in GitHub workflows with automatic Python virtualenv
activation doesn't work. Running `python` causes the workflow hangs and memory
leak.

This is just a simple reproduction by running `python`, in the actual use case
other `uv` related commands were run and failed.

## Current behavior

The step `python --version` in `.github/workflows/mise.yaml` hangs and got
killed eventually.

When running remotely on GitHub, the step failed with exit code 143
([run](https://github.com/CHC383/mise-github-action-debug/actions/runs/16331542152/job/46135072525)).

When running locally with [act](https://nektosact.com/) (through
[GitHub Local Actions](https://sanjulaganepola.github.io/github-local-actions-docs/)
in VSCode), the log has a bit more information as shown below, and the Docker
container reached the memory limit and got OOMKilled.

```
⭐ Run Main python --version
  🐳  docker exec cmd=[bash -e /var/run/act/workflow/4] user= workdir=
mise ERROR /opt/hostedtoolcache/uv/0.7.21/x86_64/uv failed
mise WARN  uv venv failed: /opt/hostedtoolcache/uv/0.7.21/x86_64/uv exited with non-zero status: no exit status
Python 3.13.5
  ✅  Success - Main python --version [4m5.44525175s]
```

## Expected behavior

`mise` automatically activates `uv` virtualenv without any issues.
