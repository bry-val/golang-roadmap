**Title:** Week 4: Interfaces & OOP in Go — Mar 16–20  
**Labels:** `phase-1`, `week-4`  
**Milestone:** Phase 1 — Go Foundations  
**Assignee:** @bry-val

---

## Goal

Understand Go's structural (implicit) interface system, use the standard library's most important interfaces, and learn how embedding replaces classical inheritance.

---

## Monday, Mar 16 — Interface Fundamentals

- [ ] Define an `Animal` interface with `Sound() string` and `Move() string`
- [ ] Implement it with `Dog` and `Bird` structs — note you write no `implements` keyword
- [ ] Assign a `Dog` value to an `Animal` variable; observe the dynamic dispatch
- [ ] Write a `Describe(a Animal)` function and call it with both implementations
- [ ] Define the empty interface `interface{}` (and its `any` alias) and store different types in a slice
- [ ] Tour of Go — complete **Methods → Interfaces**, **Methods → Interface values**
- [ ] Journal: explain structural typing in one paragraph and contrast it with Java/C# nominal typing

## Tuesday, Mar 17 — Type Assertions & Type Switches

- [ ] Use a type assertion `v, ok := i.(Dog)` — handle both the truthy and falsy cases
- [ ] Observe a panic when using a non-ok type assertion on the wrong type
- [ ] Rewrite the panic-prone code with the comma-ok form
- [ ] Write a `printType(i any)` function using a `switch v := i.(type)` block covering `int`, `string`, `bool`, and a default
- [ ] Use a type switch to implement a generic `sum(vals []any) float64` that handles `int`, `float64`, and `string` (try `strconv.ParseFloat`)
- [ ] Tour of Go — complete **Methods → Type assertions** and **Methods → Type switches**
- [ ] Journal: when should you prefer a type switch over multiple `errors.As` calls?

## Wednesday, Mar 18 — Standard Library Interfaces

- [ ] Implement `io.Reader` from scratch: `type StringReader struct{ s string; pos int }` with a `Read(p []byte) (n int, err error)` method; return `io.EOF` at end
- [ ] Wrap your `StringReader` in `bufio.NewReader` and read lines with `ReadString('\n')`
- [ ] Implement `io.Writer` with a `ByteCounter` that counts bytes written; use it with `fmt.Fprintf`
- [ ] Implement `fmt.Stringer` on three of your own types and verify `fmt.Println` uses your `String()` method
- [ ] Implement `sort.Interface` (`Len`, `Less`, `Swap`) for a `ByAge []Person` type; call `sort.Sort`
- [ ] Read: [io package docs](https://pkg.go.dev/io) — skim `Reader`, `Writer`, `ReadWriter`, `Closer`, `ReadCloser`
- [ ] Journal: why does Go's standard library rely so heavily on small, composable interfaces?

## Thursday, Mar 19 — Embedding & Interface Composition

- [ ] Embed `io.Reader` and `io.Writer` in a custom `ReadWriter` interface — note that no extra code is needed
- [ ] Embed a `Logger` struct inside a `Server` struct; call promoted methods directly on `Server`
- [ ] Override a promoted method by defining the same method on the outer struct
- [ ] Embed an interface in a struct to create a partial implementation (useful for test mocks)
- [ ] Write a `Middleware` pattern: define a `Handler` interface, implement it with a real handler, then wrap it with a logging decorator that also implements `Handler`
- [ ] Journal: describe one case where struct embedding could be mistaken for inheritance — and why it isn't

## Friday, Mar 20 — Mini-Project: Pluggable Formatter

- [ ] Define a `Formatter` interface: `Format(data map[string]any) ([]byte, error)`
- [ ] Implement `JSONFormatter` (using `encoding/json`) and `TextFormatter` (key=value lines)
- [ ] Add a `FormatterRegistry` that stores formatters by name and selects by name string
- [ ] In `main.go`: accept a `--format` flag (`json` or `text`), load a hard-coded data map, format it, and print to stdout
- [ ] Write interface-based tests: create a `MockFormatter` that records calls and assert it was called once with the correct data
- [ ] Run `go test -v ./...` — all tests pass; run `go vet ./...` — no findings
- [ ] Journal: weekly retrospective — what is the single most powerful idea you learned this week?

---

## Resources

- [A Tour of Go — Interfaces](https://go.dev/tour/methods/9)
- [Go by Example — Interfaces](https://gobyexample.com/interfaces)
- [Effective Go — Interfaces and types](https://go.dev/doc/effective_go#interfaces_and_types)
- [io package docs](https://pkg.go.dev/io)
