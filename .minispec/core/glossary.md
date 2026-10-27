# Glossary

- **Tool**: what the server offers a client, with a name, a description for the model, schemas and annotations.
- **Requirement**: a program the person installs apart on their computer (Docker, ffmpeg), which the server checks and explains but never installs.
- **Extension**: the folder in agent-extensions that runs this server for an agent (and Claude Code), with its skills and capabilities.
- **Capability**: what an extension lets an agent do, for the person: its skills plus its tools.

- **Test**: a Teuton folder with `start.rb` (its groups and targets) and `config.yaml` (its cases).
- **Target**: one thing a test checks, with its weight, the command that checks it (`run`) and what it expects.
- **Case**: one student (or team) in `config.yaml`, with its members (`tt_members`) and their machines.
- **Panel**: a teuton-panel, the web panel that runs Teuton for a class in session.
