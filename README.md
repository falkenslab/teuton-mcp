<div align="center">

<img src="https://raw.githubusercontent.com/falkenslab/teuton-mcp/main/docs/static/img/logo.svg" alt="teuton-mcp logo" width="112"/>

# teuton-mcp

**Your AI agent checks your students' machines with Teuton, and tells you who did what.**<br/>
Tests written from a practice, checked, run for the class after your yes, results explained per student, grades ready for Moodle, and a teuton-panel driven from the chat.

![Node.js 20+](https://img.shields.io/badge/Node.js-20%2B-339933?logo=node.js&logoColor=white)
![MCP server](https://img.shields.io/badge/MCP-server-0b0b0b)
![Teuton 3.x](https://img.shields.io/badge/Teuton-3.x-2E7D32)
![Status: in development](https://img.shields.io/badge/status-in%20development-d97706)
[![License: MIT](https://img.shields.io/badge/license-MIT-16a34a)](LICENSE)

</div>

teuton-mcp is an MCP server for [Teuton](https://github.com/teuton-software/teuton), the infrastructure test tool for system administration teachers: an AI agent writes a test from your practice (its targets, the commands that check them, their weights), checks it, runs it against your students' machines once you say yes, reads each student's results (which targets passed, which failed and why), and hands the grades to Moodle through the moodle-teacher extension. With a [teuton-panel](https://github.com/fvarrui/teuton-panel) running in your classroom, it reads the class's results and starts runs there too. Your students' passwords never reach the AI. **It's in development and not on npm yet.**

## ✨ Why teuton-mcp

- 🧪 **Tests from your practice.** Targets, commands and expectations in Teuton's language, checked before they run.
- ✋ **Nothing runs without your yes.** Running a test executes it on your computer and on your students' machines: the server asks you first, every time.
- 🔐 **Passwords stay out.** The machines' credentials in `config.yaml` are never shown to the AI.
- 📋 **Results you can act on.** Each student's grade and every target with what it expected and what it got.
- 🎓 **Grades to Moodle.** Teuton's `moodle.csv`, ready for moodle-teacher's grade import.
- 🖥️ **Your teuton-panel too.** The class in session: its results, runs, students and grades.

## 🧰 What's inside (planned)

| Area | For example |
| --- | --- |
| 🧪 Tests | `new_test`, `check_test`, `test_readme`, `list_cases` |
| ▶️ Running | `run_test` (asks first), `read_results`, `grades_csv` |
| 🖥️ teuton-panel | `panel_status`, `panel_results`, `panel_start_run`, `panel_grades_csv` |
| 🔌 For agents | The `teuton` extension in [agent-extensions](https://github.com/falkenslab/agent-extensions), with its skills and capabilities |

## 🛠️ Developing

The plan is in [`.minispec/features/teuton-tools.md`](.minispec/features/teuton-tools.md) and the main decisions in [ADR-005](.minispec/decisions/ADR-005-running-asks-the-person.md) and [ADR-006](.minispec/decisions/ADR-006-cli-and-panel.md); `CLAUDE.md` lists every command. `npm run build`, `npm test` and `npm run check` before every commit. Releases are published to npm by the owner.

<div align="center">

Made with 💖 by Falken's Lab Team

</div>
