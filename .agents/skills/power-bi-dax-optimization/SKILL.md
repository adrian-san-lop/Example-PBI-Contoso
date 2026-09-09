---
name: power-bi-dax-optimization
description: Analyze and optimize Power BI DAX formulas for performance, readability, maintainability, and safe error handling. Use when reviewing, writing, or refactoring DAX measures in this PBIP project.
---

# Power BI DAX Formula Optimization

## Quick workflow

1. Confirm the measure's business purpose, filter context, and related tables.
2. Check expensive iterators, repeated expressions, context transitions, and
   column-versus-measure references.
3. Refactor with descriptive `VAR` blocks, `DIVIDE`, explicit filter logic,
   and appropriate aggregation functions.
4. Return the optimized DAX, explain the changes, and identify edge cases.
5. Validate the measure with a representative DAX query in the connected PBIP
   model.

Keep existing business semantics and blank behavior unless a change is
explicitly requested. Use the detailed checklist and output template in
[reference.md](reference.md) when the formula needs a full review.

## Project guidance

- Keep measures in the `Measures` table when they are reusable finance KPIs.
- Follow the model's existing table and column names exactly.
- Prefer base measures and reuse them in dependent measures.
- Do not expose credentials or local file paths in examples or output.

