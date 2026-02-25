**Title:** Week 1: Go Toolchain & Language Foundations — Feb 25–28  
**Labels:** `phase-1`, `week-1`  
**Milestone:** Phase 1 — Go Foundations  
**Assignee:** @bry-val

---

## Goal

Get the Go toolchain running and build confidence with the language's basic building blocks: variables, types, control flow, and functions.

> **Note:** February 2026 jumps from Feb 28 to Mar 2 — there is no Feb 29.  
> Thursday and Friday tasks are consolidated into the Feb 28 session.

---

## Monday, Feb 25 — Environment & Hello World

- [ ] Verify Go installation: `go version` prints the expected version
- [ ] Create `week01/` package directory inside your workspace
- [ ] Write a `main.go` that prints "Hello, Go roadmap!" and run it with `go run .`
- [ ] Run `go build -o hello .` and execute the binary directly
- [ ] Read: [How to Write Go Code](https://go.dev/doc/code) (modules, workspaces, `go build`)
- [ ] Tour of Go — complete **Basics → Packages** and **Basics → Imports** sections
- [ ] Journal: note one thing that surprised you about Go's tooling vs other languages

## Tuesday, Feb 26 — Variables, Types & Constants

- [ ] Declare variables with `var`, short-declaration `:=`, and package-level `var` blocks
- [ ] Experiment with zero values for `int`, `float64`, `bool`, `string`, and pointers
- [ ] Use `const` for untyped and typed constants; observe iota in a `const` block
- [ ] Convert between numeric types explicitly; observe a compile error when you don't
- [ ] Write a small program that prints a formatted table of type zero-values using `fmt.Printf`
- [ ] Tour of Go — complete **Basics → Variables**, **Basics → Types**, **Basics → Constants**
- [ ] Journal: explain in one paragraph why Go has no implicit type coercion

## Wednesday, Feb 27 — Control Flow

- [ ] Write `for` loops: classic C-style, condition-only (while), and infinite (`for {}`)
- [ ] Range over a string and print each rune's index and Unicode code point
- [ ] Write an `if/else` chain and a `switch` statement (with and without a condition)
- [ ] Use `switch` with a `fallthrough` clause; note the difference vs default behaviour
- [ ] Write a short program that uses `goto` — then refactor it away and note why it's avoided
- [ ] Tour of Go — complete **Flow control** section
- [ ] Journal: compare Go's `for` with loops from a language you already know

## Thursday–Friday, Feb 28 — Functions & Packages (consolidated session)

- [ ] Write functions with multiple return values: `func divide(a, b float64) (float64, error)`
- [ ] Use named return values and a bare `return` — then note when that hurts readability
- [ ] Write a variadic function: `func sum(nums ...int) int`
- [ ] Create a second file in `week01/` and call an exported function from `main.go`
- [ ] Use `defer` to print "done" after a function returns; stack multiple defers and observe order
- [ ] Create a separate `mathutil` package in `week01/mathutil/`, export `Add` and `Multiply`
- [ ] Import your local `mathutil` package from `main.go` using the module path
- [ ] Run `go vet ./...` and `gofmt -d .` — fix any issues reported
- [ ] Write a `_test.go` file with one table-driven test for `mathutil.Add` and run `go test ./...`
- [ ] Journal: weekly retrospective — what clicked, what still feels fuzzy, what to review

---

## Resources

- [A Tour of Go — Basics](https://go.dev/tour/basics/1)
- [Go by Example — Variables](https://gobyexample.com/variables)
- [Go by Example — Functions](https://gobyexample.com/functions)
- [Effective Go — Names](https://go.dev/doc/effective_go#names)
