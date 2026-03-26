# GitHub Actions Workflow — Security Pipeline

## File: `security-pipeline.yml`

This workflow runs daily security scans on the OpenClaw codebase and generates summary reports.

## Triggers

- **Schedule:** Daily at 05:00 UTC
- **Manual:** Via GitHub Actions UI with `workflow_dispatch`
  - Input: `scan_type` (full_scan, external_scan, internal_scan)
- **On push:** Currently disabled (can be enabled)

## What It Does

1. **Checks out code** — Fetches the latest repository
2. **Installs tools:**
   - Trivy (vulnerability scanner)
   - Hadolint (Dockerfile linter)
3. **Runs scans:**
   - `trivy fs .` — Scans filesystem for CVEs, secrets, misconfigurations
   - `hadolint Dockerfile*` — Lints Dockerfiles
4. **Parses results** — Extracts critical findings and vulnerabilities
5. **Generates report** — Creates `reports/YYYY-MM-DD.md` with:
   - Verdict (PASS/FAIL)
   - Critical findings
   - Warnings
   - Recommendations
6. **Commits and pushes** — Adds the report to the `reports/` folder

## Output

Reports are saved to `reports/YYYY-MM-DD.md` with format:

```markdown
# OpenClaw Security Report — YYYY-MM-DD

## Verdict: PASS/FAIL

## Critical Findings
- [CRITICAL] vulnerability description
  Fix: update to version X

## Warnings
- Warning description

## Recommendations
- Actionable steps
```

## Example Run

```bash
# Manual trigger with scan type
gh workflow run security-pipeline.yml -f scan_type=full_scan
```

## Permissions

- **Contents:** write (to commit reports)
- **Actions:** read (to get workflow context)

## Notes

- The workflow only scans the repository code, not the live server
- For system-level scans (Lynis, Rkhunter, ClamAV), see `server_report/` folder
- Secrets scanning is enabled — results are in Trivy output

---
*Part of OpenClaw Security Pipeline*