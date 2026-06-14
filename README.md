# Task Output Folder Skill

Task Output Folder is a reusable workflow for AI agents and maintainers who need a predictable place for generated deliverables, scratch files, staging copies, exports, previews, and other task-local artifacts.

## What It Solves

Agents often create ad hoc folders such as `work/`, `scratch/`, `tmp/`, or `output/` while working. That makes later cleanup and review harder. This skill standardizes those files under a timestamped folder inside `task-outputs/`, while leaving existing project source files in their natural locations.

## Package Contents

```text
task-output-folder-skill/
  README.md
  SKILL.md
```

There are no required scripts, assets, or external dependencies.

## How To Use

Give `SKILL.md` to an AI agent or maintainer before a task that may create generated files without an explicit destination.

Use the workflow when a task creates:

- generated reports, decks, PDFs, spreadsheets, images, archives, or exports,
- temporary staging copies for skills, plugins, templates, documents, or repositories,
- scratch scripts, temporary datasets, extracted assets, rendered previews, or validation artifacts.

Do not use it for pure chat, analysis-only answers, or ordinary in-place edits to an existing codebase unless the task also creates new artifacts.

## Safety Notes

- If the user gives an explicit output path, use that path instead.
- Do not move existing project source files into `task-outputs/`.
- Do not store dependency folders, caches, virtual environments, or build outputs there unless the user explicitly requested them as deliverables.
- Do not leave unrelated ad hoc staging folders behind after the task is complete.
