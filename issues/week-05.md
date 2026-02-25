**Title:** Week 5: Goroutines & Channels Basics — Mar 23–27  
**Labels:** `phase-1`, `week-5`  
**Milestone:** Phase 1 — Go Foundations  
**Assignee:** @bry-val

---

## Goal

Launch goroutines confidently, communicate between them with channels, and handle common concurrency patterns (fan-out, timeouts, cancellation) without data races.

---

## Monday, Mar 23 — Goroutines

- [ ] Launch 5 goroutines that each print their index; observe the non-deterministic output order
- [ ] Fix the loop-capture bug: use a loop variable copy or pass `i` as a goroutine parameter
- [ ] Use `time.Sleep` in the main goroutine to wait — then note why this is unreliable
- [ ] Use `sync.WaitGroup` instead: `wg.Add(1)` before each goroutine, `wg.Done()` inside, `wg.Wait()` in main
- [ ] Check GOMAXPROCS: print `runtime.GOMAXPROCS(0)` and experiment with setting it to 1
- [ ] Tour of Go — complete **Concurrency → Goroutines**
- [ ] Journal: what is the difference between concurrency and parallelism in the context of Go's scheduler?

## Tuesday, Mar 24 — Channels

- [ ] Create an unbuffered channel `ch := make(chan int)`; send and receive in separate goroutines
- [ ] Observe a deadlock when you send on an unbuffered channel without a receiver — read the fatal error
- [ ] Create a buffered channel `make(chan int, 5)`; fill it without blocking, then drain it
- [ ] Use `range ch` to receive until the channel is closed; call `close(ch)` from the sender goroutine
- [ ] Write a `generate(nums ...int) <-chan int` pipeline stage that sends ints and closes when done
- [ ] Write a `square(in <-chan int) <-chan int` stage that reads from `in` and sends squares
- [ ] Chain `generate` → `square` → `range` in `main`
- [ ] Tour of Go — complete **Concurrency → Channels** and **Concurrency → Buffered Channels**
- [ ] Journal: when would you choose a buffered channel over an unbuffered one?

## Wednesday, Mar 25 — Select & Timeouts

- [ ] Use `select` to receive from two channels simultaneously and print whichever arrives first
- [ ] Add a `default` case to `select` to make it non-blocking
- [ ] Implement a timeout using `select` and `time.After(2 * time.Second)`: cancel a slow operation
- [ ] Write a `ticker` loop: use `time.NewTicker` and a `select` with a quit channel to stop it
- [ ] Implement a `merge(cs ...<-chan int) <-chan int` fan-in function using goroutines and a `select`
- [ ] Tour of Go — complete **Concurrency → Select**
- [ ] Journal: explain the difference between `time.After` and `time.NewTimer` — when does the latter avoid a goroutine leak?

## Thursday, Mar 26 — sync Primitives: WaitGroup & Mutex

- [ ] Write a shared counter incremented by 100 goroutines without synchronisation; run with `-race` and observe the data race
- [ ] Fix the race with `sync.Mutex`: wrap the increment in `mu.Lock()` / `mu.Unlock()`
- [ ] Rewrite using `sync.RWMutex`: allow concurrent reads and exclusive writes
- [ ] Use `sync.Once` to initialise an expensive singleton exactly once across 10 goroutines
- [ ] Use `sync.WaitGroup` to fan out 10 workers and collect results in a slice (protect the slice with a mutex)
- [ ] Tour of Go — complete **Concurrency → sync.Mutex**
- [ ] Journal: describe one scenario where `sync.RWMutex` outperforms `sync.Mutex` significantly

## Friday, Mar 27 — Mini-Project: Concurrent Directory Scanner

- [ ] Write a `scan(root string, results chan<- string, wg *sync.WaitGroup)` function that walks a directory tree with `filepath.WalkDir`
- [ ] For each `.go` file found, launch a goroutine that counts lines and sends `"path:linecount"` to `results`
- [ ] Collect all results in `main` and print a sorted summary table
- [ ] Run the program with the `-race` flag: `go run -race . ~/code`; resolve any data races found
- [ ] Write at least two tests: one for an empty directory and one with a known tree fixture
- [ ] Benchmark single-threaded vs concurrent scan on a directory with ≥ 50 files
- [ ] Run `go test -v -race ./...` — all tests pass with no races
- [ ] Journal: weekly retrospective — what was the most confusing concurrency bug you hit, and how did `-race` help?

---

## Resources

- [A Tour of Go — Concurrency](https://go.dev/tour/concurrency/1)
- [Go Blog — Go Concurrency Patterns](https://go.dev/blog/pipelines)
- [Go by Example — Goroutines](https://gobyexample.com/goroutines)
- [Go by Example — Channels](https://gobyexample.com/channels)
- [Go by Example — Select](https://gobyexample.com/select)
