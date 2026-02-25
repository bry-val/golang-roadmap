**Title:** Week 7: Testing in Go — Apr 6–10  
**Labels:** `phase-1`, `week-7`  
**Milestone:** Phase 1 — Go Foundations  
**Assignee:** @bry-val

---

## Goal

Write professional-grade tests using Go's standard `testing` package — table-driven tests, subtests, benchmarks, examples, and coverage — and mock dependencies cleanly via interfaces.

---

## Monday, Apr 6 — The `testing` Package & Table-Driven Tests

- [ ] Write a `Calculator` package with `Add`, `Sub`, `Mul`, `Div` functions
- [ ] Write a `_test.go` file with one simple test per function using `t.Errorf`
- [ ] Convert the tests to a single table-driven test using `[]struct{ name, input, want }` and `t.Run`
- [ ] Run `go test -v ./...` and read the output format; run `go test -run TestCalculator/Div ./...` to filter
- [ ] Add a test that deliberately fails; observe the output; revert the failure
- [ ] Use `t.Fatal` and `t.Error` — note the difference in execution flow
- [ ] Read: [Go Blog — The Go Testing Package](https://go.dev/doc/code#Testing)
- [ ] Journal: why are table-driven tests preferred over one test per case in idiomatic Go?

## Tuesday, Apr 7 — Subtests & Test Helpers

- [ ] Refactor the calculator tests to use `t.Run` subtests with clear names (e.g. `"2+3=5"`)
- [ ] Mark two independent subtests with `t.Parallel()` and verify they run concurrently (add `time.Sleep` to observe)
- [ ] Write a `testhelper.go` file with a `AssertEqual[T comparable](t *testing.T, got, want T)` generic helper; call `t.Helper()` inside it
- [ ] Use `testing.TB` as the parameter type in the helper so it accepts both `*testing.T` and `*testing.B`
- [ ] Write a `setup()` and `teardown()` pair using `t.Cleanup(func())` — test that `Cleanup` runs even on failure
- [ ] Journal: what does `t.Helper()` do to stack traces and why does it matter?

## Wednesday, Apr 8 — Benchmarks & the `-bench` Flag

- [ ] Write `BenchmarkAdd(b *testing.B)` for the calculator; run with `go test -bench=. -benchtime=3s`
- [ ] Use `b.N` correctly in the loop: `for i := 0; i < b.N; i++`
- [ ] Add `b.ReportAllocs()` and run with `-benchmem` to see heap allocations per operation
- [ ] Write a benchmark comparing a string concatenation with `+` vs `strings.Builder` for 1000 iterations
- [ ] Use `b.ResetTimer()` after expensive setup to exclude setup time from measurements
- [ ] Run `go test -bench=. -cpuprofile cpu.out` and inspect with `go tool pprof -top cpu.out`
- [ ] Journal: what is the significance of `allocs/op` and `B/op` in benchmark output?

## Thursday, Apr 9 — Coverage & Testable Examples

- [ ] Run `go test -cover ./...` to see coverage percentages; aim for > 80% in the calculator package
- [ ] Run `go test -coverprofile=cover.out ./... && go tool cover -html=cover.out` to view the HTML coverage report
- [ ] Identify one uncovered branch; write a test to cover it
- [ ] Write a `ExampleAdd()` function in `example_test.go`; add the `// Output:` comment; run `go test` to verify it passes as documentation
- [ ] Write a `ExampleCalculator_Div_zero()` showing divide-by-zero error handling
- [ ] Read: [Go Testing docs — Examples](https://pkg.go.dev/testing#hdr-Examples)
- [ ] Journal: how do testable examples serve as both tests and documentation simultaneously?

## Friday, Apr 10 — Mocking with Interfaces & Mini-Project

- [ ] Define a `Storage` interface with `Save(key, val string) error` and `Load(key string) (string, error)`
- [ ] Write a production `FileStorage` implementation
- [ ] Write a `MemoryStorage` test double that stores data in a map — no file system needed in tests
- [ ] Wire `MemoryStorage` into your unit tests for a `UserService` that depends on `Storage`
- [ ] Use `t.TempDir()` to create a real temp directory for integration tests that use `FileStorage`
- [ ] Create a fully tested `StringProcessor` package: `Reverse`, `WordCount`, `IsPalindrome` with table-driven tests, benchmarks, and examples for each function
- [ ] Run `go test -v -race -count=1 -coverprofile=cover.out ./...` — 100% coverage, zero races
- [ ] Journal: weekly retrospective — what testing habit will you enforce in every future Go project?

---

## Resources

- [Go Blog — Testing Flags](https://pkg.go.dev/testing)
- [Go by Example — Testing](https://gobyexample.com/testing)
- [Go by Example — Benchmarks](https://gobyexample.com/testing-and-benchmarking)
- [Dave Cheney — Prefer table driven tests](https://dave.cheney.net/2019/05/07/prefer-table-driven-tests)
