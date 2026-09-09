# Repository Guidelines

## Project Structure

This repository is a Power BI Project (PBIP) for the Contoso example. Open
`PBI-Example-contoso.pbip` from the repository root in Power BI Desktop. The
semantic model is in `PBI-Example-contoso.SemanticModel/definition/` (TMDL
model, database, and cultures). The report definition is in
`PBI-Example-contoso.Report/definition/`, with pages stored below `pages/`.
Themes and shared assets are under `PBI-Example-contoso.Report/StaticResources/`.

The local CSV inputs are in `src/`. `src-backup/`, Power BI cache files, and
local settings are intentionally ignored by Git; never commit datasets,
archives, or credentials.

## Development and Validation

- Open the project: `start PBI-Example-contoso.pbip`.
- Inspect repository files: `rg --files`.
- Check ignored local data: `git status --short --ignored`.
- Check whitespace before committing: `git diff --check`.
- Connect to the open PBIP with the Power BI modeling MCP when model changes
  need to be automated, then refresh affected tables and validate with a DAX
  query.

There is no package manager or separate build pipeline. Power BI Desktop is the
development and runtime validation environment.

## Skills and Progressive Disclosure

Project skills live under `.agents/skills/<skill-name>/`. The DAX optimization
skill starts at
`.agents/skills/power-bi-dax-optimization/SKILL.md`; read its linked
`reference.md` only when a full formula review or output template is needed.
Keep the main `SKILL.md` focused on triggers and the short workflow, and place
extended checklists or examples in one-level-deep reference files.

## Style and Naming

Preserve Power BI generated filenames and identifiers unless a rename is
intentional. Keep JSON at two-space indentation and retain the existing
tab-indented TMDL style. Prefer focused edits and avoid formatting churn in
generated PBIR/TMDL files. Use clear business names such as `Sales`, `Customer`,
and `Date` for model objects.

## Testing

Open the PBIP in Power BI Desktop, refresh the semantic model after source or
Power Query changes, and inspect affected report pages. For text-only changes,
run `git diff --check` and review the changed PBIR/TMDL files. No automated test
suite is currently configured.

## Commits and Pull Requests

Use short conventional prefixes already present in history, such as
`feat/...`, `fix/...`, and `chore/...`. Pull requests should describe the PBIP
area changed, the Power BI Desktop validation performed, and any visual impact.
Include screenshots for report visual changes and confirm that local data
folders remain excluded.
