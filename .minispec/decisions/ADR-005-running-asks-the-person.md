# ADR-005: running a test asks the person, and passwords never reach the model

## Status

Accepted (27 October 2026).

## Context

A Teuton test's `start.rb` is Ruby: `teuton run` executes it on the person's computer, and its `run` commands reach the machines in `config.yaml` (students' machines, over SSH or Telnet). An agent can write that file and call the run, so running is executing code, locally and on others' machines. `config.yaml` also holds those machines' credentials (`host1_password: secret_1`) and the students' names (`tt_members`).

## Decision

- `run_test` (and starting a run in a panel) asks the person itself through MCP elicitation before running: the test's folder, its targets' count, which cases (all, or the ones given) and their hosts, and the config file. Declined, nothing runs. An app without elicitation can't run tests, unless the server was started with `TEUTON_MCP_CONFIRM=client` (an app that already asks before every call), as moodle-mcp and docker-mcp do.
- `check_test` must pass first: `run_test` runs `teuton check` itself and refuses a test it rejects.
- Nothing the server returns carries a password or a key: case listings, results and errors redact every config value whose key names a password, secret, token or key (`*_password`, `*_pass`, `*_secret`, `*_token`, `*_key`), and the agent is told never to read `config.yaml` with its own file tools.
- Students' names come as they are in `tt_members`: the agent's own rules about students' data apply (miyagi's), not this server's.

## Consequences

- One question per run, the server's: the extension lists `run_test` in `serverConfirmTools`.
- Running in a container (Docker) was weighed and left out for now: the person runs Teuton locally today, as teuton-panel does.
