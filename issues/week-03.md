**Title:** Week 3: Functions & Error Handling — Mar 9–13  
**Labels:** `phase-1`, `week-3`  
**Milestone:** Phase 1 — Go Foundations  
**Assignee:** @bry-val

---

## Goal

Deepen knowledge of Go functions (first-class values, closures, defer/panic/recover) and adopt Go's idiomatic error-handling philosophy — explicit propagation, wrapping, and sentinel errors.

---

## Monday, Mar 9 — First-Class Functions & Closures

- [ ] Assign a function to a variable: `double := func(x int) int { return x * 2 }`
- [ ] Pass a function as an argument: implement `Map`, `Filter`, and `Reduce` for `[]int`
- [ ] Write a closure that acts as a counter: `newCounter() func() int`
- [ ] Write a closure-based memoisation wrapper for an expensive `fib(n int) int`
- [ ] Observe a loop-variable capture bug (pre-Go 1.22) and the fix using a local copy or parameter
- [ ] Tour of Go — complete **Methods → Function values** and **Methods → Function closures**
- [ ] Journal: write one concrete use-case where a closure is cleaner than a struct with a method

## Tuesday, Mar 10 — Defer, Panic & Recover

- [ ] Stack three `defer` calls and observe LIFO execution order
- [ ] Use `defer` to guarantee file closure in a file-reading function (`os.Open` + `f.Close`)
- [ ] Use `defer` to log function entry/exit with elapsed time
- [ ] Call `panic("something went wrong")` and observe the goroutine stack dump
- [ ] Add a `defer recover()` call and print the recovered value — note that panic unwinding stops
- [ ] Write a `safeDiv(a, b int) (result int, err error)` that converts a divide-by-zero panic into an error
- [ ] Read: [Defer, Panic, and Recover](https://go.dev/blog/defer-panic-and-recover) (official blog)
- [ ] Journal: when is it appropriate to use `panic` vs returning an `error`?

## Wednesday, Mar 11 — The `error` Interface & Custom Errors

- [ ] Inspect the `error` interface definition: `type error interface { Error() string }`
- [ ] Create a custom error type `ValidationError` with `Field` and `Message` fields; implement `Error() string`
- [ ] Use `errors.New` and `fmt.Errorf` to create and format errors
- [ ] Write a function that returns multiple errors and collect them into a slice
- [ ] Handle a `nil` error return correctly; observe what happens if you return a typed nil interface
- [ ] Tour of Go — complete **Methods → Errors**
- [ ] Journal: describe the "typed nil interface" gotcha in your own words

## Thursday, Mar 12 — Error Wrapping & Unwrapping

- [ ] Wrap an error with context: `fmt.Errorf("opening config: %w", err)`
- [ ] Use `errors.Is` to match a specific sentinel error through a chain of wraps
- [ ] Use `errors.As` to extract a `*ValidationError` from a wrapped error chain
- [ ] Define a package-level sentinel: `var ErrNotFound = errors.New("not found")`
- [ ] Implement `Unwrap() error` on a custom error type and verify `errors.Is` traverses it
- [ ] Read: [Working with Errors in Go 1.13](https://go.dev/blog/go1.13-errors) (official blog)
- [ ] Journal: write the "rule of thumb" you'll follow for when to wrap vs not wrap an error

## Friday, Mar 13 — Mini-Project: CLI Configuration Loader

- [ ] Create a `config` package with a `Load(path string) (*Config, error)` function
- [ ] Return `ErrNotFound` (wrapped) when the file is missing; return a `*ParseError` for malformed input
- [ ] Parse a simple `KEY=VALUE` file format manually (no third-party libraries)
- [ ] In `main.go`: call `Load`, use `errors.Is(err, config.ErrNotFound)` to print a friendly message, and `errors.As` to print field-level detail for `*ParseError`
- [ ] Write table-driven tests covering: file not found, malformed line, valid config, empty file
- [ ] Run `go test -v -count=1 ./...` and confirm all tests pass
- [ ] Run `go vet ./...` and resolve any findings
- [ ] Journal: weekly retrospective — identify one error-handling pattern you'll reuse in future projects

---

## Resources

- [Go Blog — Defer, Panic, and Recover](https://go.dev/blog/defer-panic-and-recover)
- [Go Blog — Working with Errors in Go 1.13](https://go.dev/blog/go1.13-errors)
- [Go by Example — Errors](https://gobyexample.com/errors)
- [Go by Example — Closures](https://gobyexample.com/closures)
