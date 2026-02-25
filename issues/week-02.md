**Title:** Week 2: Core Data Structures — Mar 2–6  
**Labels:** `phase-1`, `week-2`  
**Milestone:** Phase 1 — Go Foundations  
**Assignee:** @bry-val

---

## Goal

Master Go's built-in collection types — arrays, slices, and maps — and the `struct` type, which is the foundation of all custom data modelling in Go.

---

## Monday, Mar 2 — Arrays & Slice Fundamentals

- [ ] Declare fixed-size arrays: `var a [5]int` and `b := [3]string{"x","y","z"}`
- [ ] Observe that arrays are value types: assign one array to another and modify the copy
- [ ] Create slices with `make([]int, len, cap)` and with a literal `[]int{1,2,3}`
- [ ] Use `append` to grow a slice; print `len` and `cap` before and after each append to observe doubling
- [ ] Use the three-index slice expression `s[low:high:max]` to limit capacity
- [ ] Write a function `filter(s []int, pred func(int) bool) []int` using append
- [ ] Tour of Go — complete **More types → Arrays** and **More types → Slices**
- [ ] Journal: explain the difference between a slice's length and capacity in your own words

## Tuesday, Mar 3 — Slice Internals & Tricks

- [ ] Use `copy(dst, src)` to clone a slice; prove the copy is independent
- [ ] Implement the delete-element-by-index pattern (order-preserving and fast variants)
- [ ] Write a `chunk(s []int, size int) [][]int` function that splits a slice into batches
- [ ] Benchmark `append` vs pre-allocated slice (`make([]int, 0, n)`) for 1 million integers
- [ ] Read: [Go Slices: usage and internals](https://go.dev/blog/slices-intro) (official blog)
- [ ] Journal: describe one real-world scenario where pre-allocation avoids GC pressure

## Wednesday, Mar 4 — Maps

- [ ] Declare maps with `make(map[string]int)` and with map literals
- [ ] Perform all four CRUD operations; use the comma-ok idiom to distinguish missing keys from zero values
- [ ] Iterate over a map with `range`; note that order is non-deterministic and write a sorted-key print
- [ ] Delete a key with `delete`; access a deleted key to confirm the zero value is returned
- [ ] Write a word-frequency counter: read a string, split on whitespace, count occurrences in a map
- [ ] Attempt to write to a nil map; read the panic message and add proper initialisation
- [ ] Tour of Go — complete **More types → Maps**
- [ ] Journal: when would you choose a map over a slice of structs?

## Thursday, Mar 5 — Structs

- [ ] Define a `Person` struct with fields `Name string`, `Age int`, `Email string`
- [ ] Create values using struct literals (field names and positional), and pointer variants
- [ ] Access fields on a pointer to a struct without explicit dereferencing
- [ ] Add a `String() string` method (implements `fmt.Stringer`) and verify it prints in `fmt.Println`
- [ ] Write a constructor function `NewPerson(name string, age int) (*Person, error)` that validates inputs
- [ ] Embed an `Address` struct inside `Person` and access promoted fields
- [ ] Tour of Go — complete **More types → Structs**, **More types → Pointers**
- [ ] Journal: how is Go's struct embedding different from class inheritance?

## Friday, Mar 6 — Mini-Project: In-Memory Contact Book

- [ ] Create a `contactbook` package with a `Book` struct backed by `map[string]*Contact`
- [ ] Implement `Add(c Contact) error`, `Get(name string) (*Contact, bool)`, `Delete(name string)`, `List() []Contact`
- [ ] Write a `main.go` CLI that reads commands from stdin: `add`, `get`, `delete`, `list`
- [ ] Write table-driven tests for all four `Book` methods (`_test.go`)
- [ ] Run `go test -v ./...` and confirm all tests pass
- [ ] Run `go vet ./...` and resolve any findings
- [ ] Journal: weekly retrospective — note one tricky bug you hit and how you diagnosed it

---

## Resources

- [Go Blog — Slices Intro](https://go.dev/blog/slices-intro)
- [Go by Example — Maps](https://gobyexample.com/maps)
- [Go by Example — Structs](https://gobyexample.com/structs)
- [Effective Go — Data](https://go.dev/doc/effective_go#data)
