# dsh-awesome-preset

English | [中文](README.zh.md)

[![npm version](https://img.shields.io/npm/v/dsh-awesome-preset.svg?color=blue)](https://www.npmjs.com/package/dsh-awesome-preset)
[![license](https://img.shields.io/npm/l/dsh-awesome-preset.svg)](LICENSE)
[![GitHub release](https://img.shields.io/github/v/release/Jaylor-Wang/dsh-awesome-preset.svg)](https://github.com/Jaylor-Wang/dsh-awesome-preset/releases)
[![DeepSeek Harness](https://img.shields.io/badge/DeepSeek%20Harness-Preset-orange.svg)](https://github.com/deepseek-ai/deepseek-harness)

Ultra-lean daily coding agent preset for [DeepSeek Harness (`dsh`)](https://github.com/deepseek-ai/deepseek-harness).

## Highlights

- **Lean & Responsive**: Removes heavy orchestration layers (no file delivery tool (`present`), goals, complex plan modes, sub-agents, or TODO trackers). Focuses purely on fast, direct coding cycles.
- **Essential Tooling**: Retains core tools needed for day-to-day software development:
  - File reading, editing, and fast directory scanning (`fs`, `fs-search`)
  - Full-featured Bash execution (`tool-bash`)
  - Background asynchronous task management (`tool-jobs`)
  - External skill packs support (`skill-filesystem`, `tool-skill`)
  - On-demand context compaction & memory protection (`compaction`, `/compact`)
- **Tuned FS & Search Efficiency (Aligned with AGENTS.md)**:
  - `tool-fs-search`: caps `glob` results to ≤ 50 entries and `grep` matches to ≤ 50 (preview ≤ 500 bytes/line), preventing context flooding and utilizing spill files when exceeded.
  - `tool-fs`: `readLimit: 800` (max 600 chars/line, max 120KB), ensuring cohesive code units are read in full while preventing massive monolithic files from blowing up token windows.
- **Resilient Bash & Long-running Job Execution**:
  - `tool-bash`: enables background job support and `promoteOnTimeout: true` (smoothly promotes timed-out foreground commands into background jobs, preventing task termination and UI hangs).
  - Built-in `bash-sandbox` executor tuning & Windows adaptation (enables Bash sandbox, disables conflicting `pwsh-sandbox`, and configures 120s/600s resilient timeouts with 3s termination grace) out of the box, delegating stream output cap to global configuration or official 64KB defaults.
- **Master Persona with Operation Boundary Partitioning**: Instructs the model as a master autonomous engineer, biasing toward direct concurrent action for coding tasks while strictly isolating irreversible operations (npm publish: strictly conservative, never mutate versions, and immune to transient registry validation lag/404s without retrying in-flight publishes), ensuring both blistering local speed and rock-solid deployment safety.

## Installation

Run in your DeepSeek Harness environment:

```bash
# Recommended: install from npm
dsh plugin --profile web add dsh-awesome-preset

# Or install directly from GitHub
dsh plugin --profile web add github:Jaylor-Wang/dsh-awesome-preset
```

### Local Development / Linking

Clone locally and link directly into your profile:

```bash
git clone https://github.com/Jaylor-Wang/dsh-awesome-preset.git
dsh plugin --profile web add ./dsh-awesome-preset
```

Verify installation:

```bash
dsh plugin --profile web list
```

## Usage

1. Restart or start DeepSeek Harness (`dsh web`) to load the Cordis patch;
2. In the Web UI, open a session and select **`awesome`** from the agent preset dropdown list above the prompt input bar;
3. Start fast, distraction-free coding!

## License

[MIT](LICENSE)
