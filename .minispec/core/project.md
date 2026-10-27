# Project

**teuton-mcp**: [Teuton](https://github.com/teuton-software/teuton) for AI agents: write, check and run infrastructure tests on students' machines, read each student's results and grades, and drive a [teuton-panel](https://github.com/fvarrui/teuton-panel), through MCP.

- **What**: an MCP server over stdio, published on npm as `@falkenslab/teuton-mcp`, that an AI app (Claude Code, Codex, an agent built on agent-kit) starts with `npx`. It drives the `teuton` command (Ruby gem, 3.x) the person installs apart, and a teuton-panel running on the teacher's computer.
- **For whom**: teachers of system administration, networks and similar (miyagi's), who evaluate their students' machines. Only the teacher's side: students use teuton-panel.
- **What an agent does with it**: scaffold a test (`teuton new`), check it (`teuton check`), write its statement (`teuton readme`), list its cases without their passwords, run it for the whole class or some cases after the person's yes (`teuton run`, ADR-005), read each case's results from teuton's JSON reports (grade, targets passed and failed, why), and hand over `moodle.csv` for moodle-teacher's `import_grades`. With a panel: read the class's results, start and stop runs, manage the active test and the students, download its `moodle.csv` (ADR-006).
- **How it reaches agents**: as the `teuton` extension in [agent-extensions](https://github.com/falkenslab/agent-extensions), which pins its version, declares Ruby and teuton as requirements, adds the skills (the DSL, writing good targets, running and reading results) and the capabilities.
- **Out of scope**: the craft of designing a practice or grading it (the agent's), students' self-checks (teuton-panel's), installing Ruby or teuton (explained, never installed: ADR-004), and machines teuton can't reach.
- **Where it stands**: the template, renamed; the work is `.minispec/features/teuton-tools.md`.
