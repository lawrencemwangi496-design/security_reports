# Server Security Reports — Detailed Analysis

This folder contains deep-dive security analysis for the OpenClaw server environment, complementing the automated summaries in `../reports/`.

## Purpose

While the automated `reports/` folder gives a quick verdict, this folder provides:

- **Raw scan outputs** from Lynis, Rkhunter, ClamAV, and Trivy
- **Full threat analysis** with severity, impact, and step-by-step fixes
- **System hardening recommendations** from Lynis audits
- **Rootkit investigation** details

## Structure

```
server_report/
├── README.md                    # This file
└── YYYY-MM-DD/                  # Date-based folders
    ├── README.md                # Quick overview for that day's scan
    ├── summary.md               # Full threat analysis with fixes
    └── internal_scan/           # Raw scan outputs
        ├── lynis_report.txt     # System hardening audit
        ├── rkhunter_report.txt  # Rootkit detection
        ├── clamscan_report.txt  # Malware scan
        └── trivy_report.txt     # Dependency vulnerabilities
```

## What Each File Contains

### `README.md` (per day)
- Quick status (PASS/FAIL)
- Immediate actions summary
- Links to full analysis

### `summary.md` (per day)
- **Critical threats** — Severity, component, impact, fix commands
- **System hardening** — Kernel, SSH, filesystem recommendations
- **Rootkit warnings** — Suspicious files and investigation steps
- **Priority actions** — Ordered list of what to fix first

### `internal_scan/`
- **lynis_report.txt** — Full Lynis output with 49+ hardening suggestions
- **rkhunter_report.txt** — Rootkit scan log with warnings
- **clamscan_report.txt** — Malware scan results
- **trivy_report.txt** — Full vulnerability and secret scan

## Latest Report

[2026-03-26/](./2026-03-26/) — **Status:** ❌ FAIL
- Critical: fast-xml-parser XSS
- High: Angular, axios vulnerabilities
- 9,126 system CVEs

## How Reports Are Generated

These reports are created manually or via local scripts (not automated by GitHub Actions). They provide deeper context than the automated summaries.

---
*Maintained by OpenClaw Security Team*