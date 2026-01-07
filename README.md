# Git & GitHub Notes

## Basic Git Commands

### Pulling Changes from a GitHub Repository

**Direct pull (replaces local code without review):**
```bash
git pull origin main
```

**Fetch and merge (download, review, then merge):**
```bash
git fetch origin
git merge origin/main
```

---

## Automating Changelog Updates with GitHub Actions

### Setting Up "release-please.yml"

**Create the workflow file:**
```
.github/workflows/release-please.yml
```

**Add the following configuration:**
```yml
name: release-please
on:
  push:
    branches:
      - main
jobs:
  release-please:
    runs-on: ubuntu-latest
    steps:
      - uses: googleapis/release-please-action@v4
        with:
          release-type: java # or python, node, go, etc.
```

---

## Commit Message Convention

Release Please uses commit message prefixes to automatically update documentation and version numbers following semantic versioning (Major.Minor.Patch).

### Versioning Prefixes

#### `fix: ...`
**Purpose:** Bug fixes or patches  
**Version bump:** Patch (e.g., 1.0.0 → 1.0.1)  
**Example:**
```bash
git commit -m "fix: resolve memory leak in connection pool"
```

#### `feat: ...`
**Purpose:** New features or enhancements  
**Version bump:** Minor (e.g., 1.0.0 → 1.1.0)  
**Example:**
```bash
git commit -m "feat: add vector search capability to oracle backend"
```

#### `feat!: ...` or `fix!: ...`
**Purpose:** Breaking changes  
**Version bump:** Major (e.g., 1.0.0 → 2.0.0)  
**Example:**
```bash
git commit -m "feat!: remove deprecated API endpoints"
```

#### `chore: ...`
**Purpose:** Internal changes that don't affect functionality  
**Version bump:** None  
**Example:**
```bash
git commit -m "chore: update build dependencies"
```

---

## Quick Reference

| Prefix | Type | Version Impact | Example |
|--------|------|----------------|---------|
| `fix:` | Bug fix | Patch (x.x.X) | `fix: correct typo in error message` |
| `feat:` | New feature | Minor (x.X.x) | `feat: add dark mode support` |
| `feat!:` or `fix!:` | Breaking change | Major (X.x.x) | `feat!: redesign authentication system` |
| `chore:` | Maintenance | None | `chore: update dependencies` |
