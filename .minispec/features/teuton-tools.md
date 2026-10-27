# Writing, running and reading Teuton tests, and a teuton-panel

## Goal

A teacher's agent writes a Teuton test from a practice, checks it, runs it for the class after the teacher's yes, reads each student's results, hands the grades to Moodle, and drives a teuton-panel in session.

## Context

Decided in falkenslab/agent-extensions (27 October 2026): its own repository and npm package, the teacher's side only, local runs with the server's question (ADR-005), the CLI and a panel (ADR-006).

- **Teuton** (`gem install teuton`, Ruby ≥ 3.2; 3.3.0 on RubyGems, 26 October 2026): a test is a folder with `start.rb` (`group`, `target "…", weight:`, `run "cmd"` or `run "cmd", on: :host1`, `expect [...]`, `expect_fail`, `play do show; export end`) and `config.yaml` (`global:` and `cases:`, each case with `tt_members` and its hosts' `hostN_ip`, `hostN_username`, `hostN_password`). Commands: `teuton new DIR`, `teuton check DIR [--cname|--cpath]`, `teuton readme DIR`, `teuton run DIR [--export=json] [--case=6,16] [--cname|--cpath] [--quiet] [--no-color]`. Reports go to `var/<test>/`: `case-NN.<format>`, `resume.<format>`, `moodle.csv`. Docs: `docs/` in teuton's repository (commands, DSL, config file).
- **teuton-panel** (`../teuton-panel`, fvarrui/teuton-panel): its JSON pages and forms are listed in ADR-006; it reads Teuton's JSON reports too, so their shape is proven there.
- **Ruby and teuton**: the person installs them; `check_requirements` (the template's) says how, with their versions (ADR-004). On Windows, RubyInstaller.
- **The extension**: `teuton` in agent-extensions, with `serverConfirmTools: ["run_test", …]`, Ruby and teuton in `requirements`, and capabilities such as `machine-checking` and `practice-grades`.

## Changes

- **CLI tools**: `new_test` (scaffold a folder), `check_test` (read-only: teuton's verdict on `start.rb` and its config, as data), `test_readme` (read-only: the statement as Markdown), `list_cases` (read-only: each case's members and hosts, passwords redacted), `run_test` (all or some cases, a config file, JSON export; asks first, ADR-005), `read_results` (read-only: from the last run's JSON reports, each case's grade and every target with its result, its weight and what it expected and got; a page at a time), `grades_csv` (read-only: where `moodle.csv` is and what it holds, for moodle-teacher's `import_grades`).
- **Panel tools** (ADR-006): `panel_status` (read-only: the panel, its active test, the class), `panel_results` (read-only), `panel_students` (read-only), `panel_start_run` and `panel_stop_run` (asks first), `panel_set_test` (asks first), `panel_student` (disable or delete one: asks first), `panel_grades_csv` (download it to a local folder).
- **Requirements**: Ruby and teuton in `REQUIREMENTS`, with the versions that work; every CLI tool starts with `await needs("teuton")`.
- **Docs** (English and Spanish), the tools reference, and tests with a fake `teuton` and a fake panel.

## Acceptance

- `npm run check`, `npm test`, `npm run typecheck`, `npm run lint` pass.
- End to end against docker-lab labs: two lab containers with SSH as two students' machines; a test written from a short practice (create a user, install a package), checked, run after the person's yes; `read_results` explains one student's failed target; `moodle.csv` imported into moodle-sandbox with moodle-teacher's `import_grades`.
- No password or key appears in any tool's result, nor in an error.
- With a teuton-panel running: the class's results read, a run started (with the question) and stopped, `moodle.csv` downloaded.
- Then the `teuton` extension in agent-extensions pins the release.
