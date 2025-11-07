# Repository Guidelines

## Project Structure & Module Organization
- Root contains `README.md` for visitors and `AGENTS.md` for contributor guidance.
- Each workflow lives in its own folder (e.g., `ai-po-extraction-pipeline/`) and includes:
  - Workflow export (`*.json`) ready for n8n import.
  - Companion documentation (`readme.md`) covering setup and node notes.
  - Sample assets (e.g., `Example PO 1.PDF`) for local validation.
- Add new workflows in sibling directories using the pattern `topic-purpose-workflow/`.

## Build, Test, and Development Commands
- Import a workflow locally: `n8n import:workflow --input <path/to/workflow.json>`.
- Run a workflow once from the CLI: `n8n workflow:execute --id <workflow-id>` after importing.
- Export updates: `n8n export:workflow --id <workflow-id> --output <path>` to refresh the JSON file in this repo.
- Validate Supabase schema changes with `psql <connection-string> -f schema.sql` (keep SQL scripts under the workflow directory).

## Coding Style & Naming Conventions
- Workflow folders: lowercase words separated by hyphens (`data-sync-webhook/`).
- File names: descriptive and consistent (`invoice-router.json`, `sample-request-uk.pdf`).
- Keep Markdown documentation in English, with headings in Title Case and sections under 120 words.
- When editing workflow JSON, preserve node naming clarity (e.g., `"name": "Validate Payload"` rather than `"Function"`).

## Testing Guidelines
- Provide at least one sample input file per workflow in a `samples/` subfolder or the root of that workflow directory.
- Document manual test steps in the workflow `readme.md` under a **Testing** heading.
- After adjustments, execute the workflow with sample data and capture success screenshots or execution logs for the PR description.
- When schema changes occur, include SQL migration snippets and confirm Supabase tables align with JSON outputs.

## Commit & Pull Request Guidelines
- Commit message format: `feat:`, `fix:`, or `docs:` prefix followed by a short imperative summary (e.g., `feat: add po ingestion retries`).
- Group related changes per commit; avoid bundling multiple workflows in a single PR.
- PR checklist:
  - Summary of modifications and impacted workflows.
  - Linked issue or task reference (e.g., `Closes #12`).
  - Notes on testing performed with links to execution logs or screenshots.
  - Any new environment variables or credentials clearly listed.

## Security & Configuration Tips
- Never commit live API keys; use placeholder names in documentation (`N8N_SUPABASE_KEY`).
- Store credential setup instructions in workflow docs, not in JSON exports.
- Redact vendor data in sample files before uploading or provide synthetic examples.
