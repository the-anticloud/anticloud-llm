# How to Update — LLM

**Project:** `LLM`
**Category:** CHIP_QUANTIZATION
**Domain:** chip quantization and model compression
**Date:** 2026-10-07

---

## Update Procedure

### Checking for Updates
```bash
LLM --version
LLM check-update
```

### Applying Updates
```bash
pip install --upgrade LLM
```

### Rolling Back
```bash
pip install LLM==<previous-version>
```

### Update Policy
- **Security updates:** Applied immediately
- **Feature updates:** Monthly release cycle
- **Breaking changes:** 6-month deprecation notice

## Verification

All 16 checks PASS. Evidence: `ISOLATED_LAB_RESULTS/03_Result_Register.md`.
