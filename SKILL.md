---
name: task-output-folder
description: Create and use a per-task output folder under a current-directory task-outputs parent directory for generated files. Use whenever Codex may create, export, convert, render, download, save, or attach user-facing files or task scratch files in a local workspace and the user has not specified an exact destination. Do not trigger for pure chat, analysis-only answers, or ordinary in-place edits to an existing codebase unless the task also creates new artifacts.
---

# Task Output Folder

## Core Rule

Create a task output parent directory and a per-task output folder lazily, only when the current task first needs to write a new file and the user did not provide a save path.

If no files are created, do not create either the parent directory or a per-task folder.

If the user specifies an output directory, filename, or destination, use that destination instead of this skill's default folder.

## Folder Location

Create a parent directory named `task-outputs/` inside the current working directory unless higher-priority instructions or workspace policy require a different writable root.

Inside `task-outputs/`, create one per-task folder using this naming pattern:

```text
task-outputs/
└── task-output-YYYYMMDD-HHMMSS-short-slug/
```

- Use local time for the timestamp.
- Use a short slug from the user's task, lowercase with hyphens.
- Keep the slug concise; prefer 2-5 words.
- If `task-outputs/` already exists, reuse it.
- If a per-task folder with the chosen name already exists, append `-2`, `-3`, and so on.

## What Goes There

Put these files in the per-task folder when no explicit destination was provided:

- User-facing generated deliverables such as reports, decks, images, PDFs, spreadsheets, archives, exports, or converted files.
- Intermediate files that exist only to support this task, such as scratch scripts, temporary datasets, extracted assets, rendered previews, or validation artifacts.
- Multiple related deliverables from the same task. Reuse the same per-task folder for the whole task.

Do not move these into the task output folder:

- Existing project source files that must be edited in place to complete a coding task.
- Project dependency files, lockfiles, configuration files, tests, fixtures, or build scripts that belong in the repository.
- Tool-generated caches such as `node_modules`, `.venv`, `.next`, `dist`, `build`, or test cache directories unless the user specifically requested that artifact.

## Existing Projects

When working in an existing codebase, keep normal implementation changes in their natural project paths. Use `task-outputs/<per-task-folder>/` only for extra artifacts that Codex creates for the user or for task-local scratch material.

Examples:

- Fixing a bug in `src/`: edit `src/` directly. Do not create `task-outputs/` unless also producing a report, screenshot, patch bundle, or other new artifact.
- Creating a standalone analysis report: create `task-outputs/<per-task-folder>/` and save the report there.
- Generating an image, slide deck, spreadsheet, or PDF: create `task-outputs/<per-task-folder>/` and save all generated files there.

## Reporting Back

In the final response, mention `task-outputs/<per-task-folder>/` only if files were actually saved there.

When referencing saved files, provide the path to the file or folder. If the environment requires user-facing deliverables to be placed under a specific outputs directory, follow that higher-priority requirement and link that location instead.
