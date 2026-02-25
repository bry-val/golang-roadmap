**Title:** Project Setup: Frictionless Learning Environment  
**Labels:** `phase-1`, `setup`  
**Milestone:** Phase 1 — Go Foundations  
**Assignee:** @bry-val

---

## Goal

Eliminate all environment friction before Week 1 starts so that every study session begins with working code, not configuration.

## Checklist

### Toolchain
- [ ] Install Go (latest stable) from [go.dev/dl](https://go.dev/dl/) and verify with `go version`
- [ ] Confirm `GOPATH` and `GOROOT` are set correctly (`go env`)
- [ ] Create a dedicated workspace directory: `~/code/golang-roadmap/`
- [ ] Run `go mod init github.com/bry-val/golang-roadmap` in the workspace root

### Editor
- [ ] Install [VS Code](https://code.visualstudio.com/) or [GoLand](https://www.jetbrains.com/go/) (your preference)
- [ ] Install the **Go** extension (VS Code: `golang.go`) and accept all prompted tool installs (`gopls`, `dlv`, `staticcheck`)
- [ ] Enable format-on-save with `gofmt` or `goimports`
- [ ] Verify the debugger works: set a breakpoint in `main.go` and hit `F5`

### Shell & Git
- [ ] Alias `go test ./...` to `gt` in your shell profile (`.zshrc` / `.bashrc`)
- [ ] Create a `golang-roadmap` GitHub repository and push the initial module
- [ ] Add a `.gitignore` with `*.test`, `*.out`, `vendor/`, `bin/`

### Reference Materials
- [ ] Bookmark [A Tour of Go](https://go.dev/tour/) — complete it if you haven't already
- [ ] Bookmark [Effective Go](https://go.dev/doc/effective_go)
- [ ] Bookmark [pkg.go.dev](https://pkg.go.dev/) for standard-library docs
- [ ] Download [Go by Example](https://gobyexample.com/) for offline reference

### Weekly Rhythm
- [ ] Block 90-minute study slots Monday–Friday on your calendar for Weeks 1–8
- [ ] Create a `journal/` directory in the repo for daily notes (`YYYY-MM-DD.md`)
- [ ] Write the first journal entry: why you want to learn Go and what "success" looks like after 8 weeks
