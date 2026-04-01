# AGENTS.md

This repository stores multiple self-authored skills.
Treat each skill as a small, isolated product with its own instructions, examples, and any optional code or tests.

## Repository Shape

- Prefer one skill per directory.
- Keep each skill self-contained.
- Put the primary instruction file in `SKILL.md` unless the existing skill format says otherwise.
- Keep examples close to the instructions they support.
- Avoid broad repository-wide refactors unless they improve many skills at once.
- Treat each skill as independently shippable.
- Keep shared conventions in this file, and skill-specific exceptions in the skill directory.

## Agent Workflow

- Start by identifying the exact skill directory you are changing.
- Prefer reading `SKILL.md`, then any local README, examples, and test files.
- Make a narrow change, then verify only the affected skill or file set.
- If a fix touches multiple skills, explain why the shared change is necessary.
- Leave unrelated files alone, even if they look imperfect.
- When in doubt, ask before introducing a new convention.

## First Steps For Agents

- Inspect the target skill directory before changing anything.
- Read the skill instructions, examples, and any local test files.
- Check for repo rules in `.cursor/rules/` and `.cursorrules`.
- Check for Copilot instructions in `.github/copilot-instructions.md`.
- If those files exist, follow them and merge them with the guidance below.
- If a skill has its own README or test notes, treat those as the source of truth for that skill.

## Build / Lint / Test Commands

There is no single repo-wide build system in this workspace.
Use the command that matches the skill’s implementation language or harness.

- Repo-wide sanity check: `git diff --check`
- Markdown-only skills: `npx prettier --check "**/*.md"`
- Markdown format fix: `npx prettier --write "**/*.md"`
- YAML/JSON validation: use the language/tooling already present in that skill directory.
- If a skill includes scripts, prefer the script entry over ad hoc shell commands.

### Single Test / Focused Check

- Run only the smallest relevant check for the file you changed.
- If the skill has a dedicated test file, run that file only.
- If the skill has a script for validation, pass the narrowest possible target.
- Examples:
  - `pytest path/to/test_file.py -k test_name`
  - `node path/to/test_file.js`
  - `npx prettier --check path/to/file.md`
  - `bash path/to/test_script.sh`

### When No Tests Exist

- Verify the instruction text manually for correctness and consistency.
- Check that examples still match the described behavior.
- Confirm links, filenames, and command snippets are valid.

## Editing Priorities

- Make the smallest change that solves the problem.
- Preserve the existing voice and structure of the skill.
- Prefer updating one skill cleanly over spreading partial fixes across many skills.
- Do not rewrite content just to make it look more generic.

## Markdown Style

- Use concise headings.
- Keep line length reasonable and scan-friendly.
- Use bullets for instructions and numbered lists for ordered procedures.
- Use fenced code blocks for commands, examples, and multi-line snippets.
- Keep code fences language-tagged when possible.
- Avoid tables unless they significantly improve readability.
- Prefer ASCII punctuation unless a skill already uses localized text.

## Writing Style

- Be direct.
- Use imperative voice for instructions.
- Avoid filler like “simply” or “just”.
- State behavior, constraints, and edge cases explicitly.
- If a step is optional, say so.
- If a step is required, mark it clearly.

## Imports / Dependencies

- Only add imports or dependencies that are actually used.
- Prefer built-in tooling when it is already sufficient.
- Keep dependency surfaces small.
- If a skill uses generated code, do not hand-edit generated sections unless the workflow requires it.
- When adding scripts, prefer minimal shell that is easy to understand and maintain.

## Formatting

- Match existing formatting in the file you are touching.
- Do not reformat unrelated files.
- Keep blank lines purposeful.
- Preserve list nesting and indentation style already present in the skill.
- For command examples, show the exact invocation the agent should run.

## Types / Schemas / Structured Data

- If the skill includes typed code, keep types narrow and explicit.
- Prefer clear names over clever abstractions.
- If a schema exists, update the schema and examples together.
- Do not widen types unless there is a concrete need.
- Favor validation at the boundary rather than deep in the logic.

## Naming Conventions

- Use descriptive names for skills, files, and helper scripts.
- Prefer `kebab-case` for files and directories unless the surrounding skill uses another convention.
- Use `SCREAMING_SNAKE_CASE` only for constants that are intended to be read as constants.
- Name examples after the behavior they demonstrate.

## Error Handling

- Fail fast when input is invalid.
- Explain what went wrong and how to fix it.
- Do not swallow errors silently.
- If a command may fail for a normal reason, document that in the skill.
- Prefer actionable messages over stack traces in user-facing instructions.

## Validation Checklist

- Confirm the skill still reads cleanly after edits.
- Confirm command examples are accurate.
- Confirm any referenced paths exist.
- Confirm any included snippets still parse.
- Confirm no unrelated files changed.
- Confirm line endings and quoting match the surrounding file style.
- Confirm added examples use commands that exist in the current skill context.

## Working With Existing Rules

- If `.cursor/rules/` exists, follow those rules first for editor-specific guidance.
- If `.cursorrules` exists, treat it as repo guidance for Cursor-based agents.
- If `.github/copilot-instructions.md` exists, incorporate it for Copilot-aware workflows.
- If any of those conflict with this file, use the more specific rule for the affected file or skill.

## When In Doubt

- Read the local skill files again.
- Prefer the smallest safe edit.
- Leave a clear note for the user if a decision requires their input.
