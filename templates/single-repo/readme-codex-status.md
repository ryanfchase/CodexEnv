# README Codex Status

Add a compact `Codex Status` section to the repo `README.md`.

Recommended contents:

1. A compact status summary
   - current `codexification_stage`
   - current `operational_readiness`
   - `next_stage_target`
   - `template_version`

2. A compact ASCII stage path
   - highlight the current stage
   - make the next stage obvious

3. Remaining work
   - copy the current promotion gate from `codex-assessment.md`
   - keep it phrased as concrete next actions

4. Toolkit available now
   - shared foundation skills
   - repo-local skills if present
   - native verification commands

Recommended ASCII shape:

```text
discovered > scaffolded > standardized > [operational] > maintained
```

Practical rule:

- `README.md` should be the thin dashboard
- `codex-template.json` should be the machine-readable summary
- `codex-assessment.md` should be the detailed evidence log
- avoid full score tables in the README when they can live in `codex-assessment.md`
