# Task Output Folder Skill

A Codex skill that creates a per-task output folder under `task-outputs/` whenever Codex generates files and the user has not provided an explicit destination.

The GitHub repository is named `task-output-folder-skill` for clarity. The skill itself is named `task-output-folder`.

## Install

Clone this repository directly into your Codex skills directory using the skill name as the local folder:

```bash
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
git clone https://github.com/harokell/task-output-folder-skill.git "${CODEX_HOME:-$HOME/.codex}/skills/task-output-folder"
```

Then restart or refresh Codex so the skill can be discovered.

You can invoke it explicitly with:

```text
Use $task-output-folder when this task creates files without an explicit destination.
```

No build step or external dependency is required.

## Contents

```text
task-output-folder-skill/
  SKILL.md
  agents/openai.yaml
```
