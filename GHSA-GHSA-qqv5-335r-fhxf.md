# GitHub Advisory: GHSA-qqv5-335r-fhxf - GitHub Actions branch checkout injection in MUI Material

## Vector
GitHub Actions branch checkout injection in MUI Material in GitHub Actions workflows enables RCE.

## Affected Component
- **Package ecosystem:** actions
- **Package name:** .github/workflows/ci.yml
- **Vulnerable version range:** all versions
- **CVSS:** 9.8 (Critical)

## PoC
```yaml
name: CI
on: pull_request
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          ref: ${{ github.event.pull_request.head.ref }}
```

## Fix
Quote the ref: `ref: '${{ github.event.pull_request.head.ref }}'`
