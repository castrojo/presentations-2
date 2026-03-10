# CNCF Presentations

Archive of CNCF-related presentations plus a Go CLI tool that validates `presentations.yaml`.

## What this is

This repo contains presentation slides and a Go CLI (`cmd/main.go`) that verifies the
`presentations.yaml` index file is syntactically correct. The CLI uses
[cobra](https://github.com/spf13/cobra) and [gopkg.in/yaml.v3](https://pkg.go.dev/gopkg.in/yaml.v3).

## Prerequisites

- Go 1.20+

## Validation

```bash
go run cmd/main.go verify --file presentations.yaml
```

This is the only meaningful "build" step — same command used in CI.

## Repository structure

```
cmd/               Go CLI source (cobra, verify subcommand)
presentations.yaml  Index of all CNCF presentations (primary data file)
*.yaml / dirs/      Per-project presentation archives (kubernetes/, prometheus/, etc.)
```

## Common commands

```bash
# Verify presentations.yaml
go run cmd/main.go verify --file presentations.yaml

# Build the binary
go build -o presentations ./cmd/...

# Sync fork with upstream
git fetch upstream && git rebase upstream/main && git push origin main --force-with-lease
```

## Critical notes

- Fork is at `castrojo/presentations-2` (name conflict — `castrojo/presentations` is a personal repo)
- Upstream default branch is `main`; old fork had `master` — work off `main` only
- No Justfile — use `go run` / `go build` directly
- CI runs: `go run cmd/main.go verify --file presentations.yaml`
