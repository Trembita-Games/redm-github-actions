# RedM GitHub Actions

Reusable GitHub Actions workflows for Trembita Games RedM/RDR2 repositories.

This repository contains shared validation workflows used by public RedM/RDR2 repositories to avoid duplicating the same repository checks in every project.

## Purpose

The goal of this repository is to provide versioned reusable workflows for repository validation.

Caller repositories should reference workflows by release tag, not by branch name. This keeps downstream repositories protected from accidental validation changes.

Use a version tag when referencing reusable workflows:

```yaml
uses: Trembita-Games/redm-github-actions/.github/workflows/validate-redm-bootstrap.yaml@v0.1.0
```

Do not reference workflows from the main branch:

```yaml
uses: Trembita-Games/redm-github-actions/.github/workflows/validate-redm-bootstrap.yaml@main
```

Version tags keep caller repositories stable when this repository receives new workflow changes.

## Repository structure

```text
redm-github-actions/
├── .github/
│   └── workflows/
│       ├── validate-redm-bootstrap.yaml
│       ├── validate-redm-resources.yaml
│       ├── validate-redm-cfx-data.yaml
│       └── validate-redm-recipes.yaml
├── .editorconfig
├── .gitattributes
├── .gitignore
└── README.md
```

## Workflows

### validate-redm-bootstrap.yaml

Reusable validation workflow placeholder for bootstrap/runtime repositories.

Target repository:

```text
redm-vanilla-template
```

Expected caller workflow:

```yaml
name: Validate Repository

on:
  push:
    branches:
      - main
      - master
  pull_request:
    branches:
      - main
      - master
  workflow_dispatch:

permissions:
  contents: read

jobs:
  validate:
    uses: Trembita-Games/redm-github-actions/.github/workflows/validate-redm-bootstrap.yaml@v0.1.0
    with:
      default_profile: dev
      validate_docker: false
```

Supported inputs:

| Input | Type | Required | Default | Description |
| --- | --- | --- | --- | --- |
| `default_profile` | `string` | `false` | `dev` | Default runtime profile expected by the bootstrap repository. |
| `validate_docker` | `boolean` | `false` | `false` | Enables Docker Compose validation when implemented. |

Planned validation scope:

- Required files
- Required directories
- Runtime/generated file safety
- Git ignore rules
- Git attributes rules
- Line endings
- Bash scripts
- PowerShell scripts
- Server icon dimensions
- Config templates
- Runtime model references
- README/documentation references
- Secret placeholder safety

### validate-redm-resources.yaml

Reusable validation workflow placeholder for standalone resource repositories.

Target repository:

```text
redm-server-data
```

Supported inputs:

| Input | Type | Required | Default | Description |
| --- | --- | --- | --- | --- |
| `validate_lua` | `boolean` | `false` | `true` | Enables Lua validation checks when implemented. |

Planned validation scope:

- Resource directory structure
- Resource manifests
- Lua files
- Standalone resource rules
- Static data consistency
- README references
- Secret placeholder safety

### validate-redm-cfx-data.yaml

Reusable validation workflow placeholder for base resource data repositories.

Target repository:

```text
redm-server-data-cfx
```

Supported inputs:

| Input | Type | Required | Default | Description |
| --- | --- | --- | --- | --- |
| `validate_source_attribution` | `boolean` | `false` | `false` | Enables source attribution checks when implemented. |

Planned validation scope:

- Base resource structure
- Resource manifests
- Source attribution checks
- Runtime file safety
- README references

### validate-redm-recipes.yaml

Reusable validation workflow placeholder for txAdmin recipe repositories.

Target repository:

```text
redm-txadmin-recipes
```

Supported inputs:

| Input | Type | Required | Default | Description |
| --- | --- | --- | --- | --- |
| `validate_yaml` | `boolean` | `false` | `true` | Enables YAML validation checks when implemented. |

Planned validation scope:

- YAML files
- Recipe structure
- Recipe references
- Install flow references
- Secret placeholder safety

## Versioning

Reusable workflows must be consumed by version tag.

Example:

```yaml
uses: Trembita-Games/redm-github-actions/.github/workflows/validate-redm-bootstrap.yaml@v0.1.0
```

Recommended release flow:

1. Add or update a reusable workflow.
2. Test it against the target repository.
3. Create a release tag.
4. Update caller repositories only when they are ready to consume the new version.

## Current release

```text
No release yet.
```

The first release will be created after the bootstrap validation workflow is ready for use.

## Commit message examples

Initial repository setup:

```text
chore: initialize reusable RedM GitHub Actions repository
```

Add reusable validation workflow placeholders:

```text
chore: add reusable validation workflow placeholders
```

Add bootstrap validation workflow logic:

```text
chore: add reusable bootstrap validation workflow
```

Update documentation:

```text
docs: document reusable workflow usage
```

## Rules

All text, config, and code files should be saved as UTF-8 without BOM.

All files should end with a single trailing newline.

Reusable workflows should remain backward-compatible within the same minor version whenever possible.

Breaking changes should be released with a new version tag and adopted by caller repositories explicitly.
