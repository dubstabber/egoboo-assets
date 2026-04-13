# AGENTS.md

Additional instructions for work under `data/`.

## Content safety

- Treat content changes here as high-risk.
- Prefer narrow, auditable edits over broad renames or mass rewrites.
- Do not change large numbers of legacy files without a generated mapping or a written migration plan.
- If you discover structural content issues, document them in `refactoring-documents/` instead of only patching files silently.

## Validation expectations

- If you change module files, object data, spawn references, or shared content used across modules, run the full validator:
  - `./build/products/x64/bin/egoboo-content-validator --data-dir "$PWD/data"`
- For small, local experiments, `test.mod` is the minimum smoke check, not the final check.
- Compare validator failures against `refactoring-documents/06-validator-baseline.md` before treating them as new regressions.

## Legacy format handling

- Preserve current mount-point and overlay semantics:
  - `mp_data`
  - `mp_modules`
  - `mp_objects`
- Do not assume a missing spawn target is a parser bug. Many current failures are content-reference integrity problems.
- When fixing spawn/object mismatches, record the old name, the new target, and whether it was a typo, placeholder, alias, or deleted content.

## Reference material

- `doc/*.odt` files may contain useful historical behavior notes and should be treated as reference material.
- `backup-copy/` remains reference-only and must never be modified, even when comparing old content layouts.
