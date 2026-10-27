# ADR-006: the teuton command, and a teuton-panel when there's one

## Status

Accepted (27 October 2026).

## Context

[teuton-panel](https://github.com/fvarrui/teuton-panel) is a web panel a teacher runs on the classroom network: students register their machines, the panel runs Teuton for the class or one student, and shows the results. It only answers the teacher's computer on its teacher area, calls the `teuton` command and reads its JSON reports. Its teacher pages have `.json` versions (`/teacher(.json)`, `/teacher/results(.json)`, `/teacher/run(.json)`, `/teacher/students(.json)`), `/teacher/moodle.csv`, `/teacher/sessions/:id/moodle.csv`; its actions are HTML forms (`POST /teacher/run/start`, `/teacher/run/stop`, `/teacher/settings`, `/teacher/students/:code`, `/disable`, `/delete`, `/teacher/sessions/new`).

## Decision

- **Both**: the CLI tools work on a test folder on this computer; the panel tools work on a running panel, at `TEUTON_MCP_PANEL_URL` (default `http://localhost:4567` or whatever the panel's default is; check it), only on `localhost`/`127.0.0.1`. Without a panel there, its tools say so.
- **Through its JSON pages**: reading the class (results, students, runs, the active test), starting and stopping a run, changing the active test, managing a student (disable, delete), downloading `moodle.csv`. Where an action has no JSON form, open an issue in teuton-panel for one (a JSON `POST` with the same fields) instead of scraping HTML.
- **What needs the person's yes**: starting a run (ADR-005's question), changing the active test or the settings, disabling or deleting a student (the server asks, as for running).

## Consequences

- The extension's skills say when to use which: the CLI to write and try a test, the panel for a class in session.
- Each panel call is checked against the panel's version (its `/teacher.json` or a version endpoint): a panel too old for a tool says which version it needs.
