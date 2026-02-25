**Title:** Week 6: Advanced Concurrency — Mar 30–Apr 3  
**Labels:** `phase-1`, `week-6`  
**Milestone:** Phase 1 — Go Foundations  
**Assignee:** @bry-val

---

## Goal

Master the full sync and context toolkits, learn canonical Go concurrency patterns (worker pool, pipeline, fan-out/fan-in), and use the race detector as a safety net.

---

## Monday, Mar 30 — sync.Map & Atomic Operations

- [ ] Use `sync.Map` for a concurrent cache: `Store`, `Load`, `LoadOrStore`, `Delete`, `Range`
- [ ] Benchmark `sync.Map` vs a `map` + `sync.RWMutex` for a read-heavy workload (90% reads, 10% writes)
- [ ] Use `sync/atomic`: increment a counter with `atomic.AddInt64`, load with `atomic.LoadInt64`
- [ ] Implement a lock-free stack using `atomic.CompareAndSwapPointer` (or the typed `atomic.Pointer[T]` from Go 1.19+)
- [ ] Run all experiments with `-race`; confirm no data races
- [ ] Read: [sync package docs](https://pkg.go.dev/sync) — skim every exported type
- [ ] Journal: when would you prefer `sync.Map` over a mutex-guarded map?

## Tuesday, Mar 31 — Context Package

- [ ] Create a `context.Background()` and pass it through a call chain of three functions
- [ ] Use `context.WithCancel`: cancel a long-running goroutine from the parent; verify the goroutine exits via `<-ctx.Done()`
- [ ] Use `context.WithTimeout` to abort an HTTP request that takes too long; check `ctx.Err() == context.DeadlineExceeded`
- [ ] Use `context.WithDeadline` with an absolute time; compare behaviour with `WithTimeout`
- [ ] Use `context.WithValue` to pass a request-ID through a handler chain; retrieve it with a typed key
- [ ] Demonstrate the anti-pattern: storing mutable state in context values
- [ ] Read: [Go Blog — Contexts and structs](https://go.dev/blog/context-and-structs)
- [ ] Journal: write the rule "Context should flow…" in your own words

## Wednesday, Apr 1 — Worker Pool Pattern

- [ ] Design a fixed-size worker pool: N goroutines reading from a shared `jobs <-chan Job` channel
- [ ] Each worker sends its result to a `results chan<- Result` channel
- [ ] Use a `sync.WaitGroup` to close `results` after all workers finish
- [ ] Feed 100 jobs (simulate with `time.Sleep(randomDuration)`) and collect all results in order
- [ ] Add graceful shutdown: send a cancel signal via `context.WithCancel` and drain in-flight jobs
- [ ] Measure throughput: jobs/second with pool sizes 1, 2, 4, 8; print a table
- [ ] Journal: explain the relationship between pool size, job duration, and CPU-bound vs I/O-bound work

## Thursday, Apr 2 — Pipeline & Fan-Out / Fan-In

- [ ] Build a three-stage pipeline: `generate` → `process` → `sink` using typed channels
- [ ] Fan out: distribute `process` across N workers each reading from the same input channel
- [ ] Fan in: merge N output channels into a single channel using a `merge` function with goroutines and `sync.WaitGroup`
- [ ] Add context cancellation to all stages so the pipeline tears down cleanly when cancelled
- [ ] Run the full pipeline with `-race`; confirm zero races
- [ ] Read: [Go Blog — Go Concurrency Patterns: Pipelines and cancellation](https://go.dev/blog/pipelines)
- [ ] Journal: draw (ASCII art or text) the data-flow diagram for your pipeline

## Friday, Apr 3 — Mini-Project: Concurrent Word-Count Server

- [ ] Accept file paths as CLI arguments; process each file concurrently in a worker pool (pool size = `runtime.NumCPU()`)
- [ ] Each worker counts word frequencies in its file and sends a `map[string]int` to a results channel
- [ ] Merge all maps in the main goroutine; print top-10 words sorted by count
- [ ] Respect a `--timeout` flag using `context.WithTimeout`; print a partial result if the deadline is hit
- [ ] Write tests: one for the merge logic, one for single-file word counting, one for timeout behaviour
- [ ] Run `go test -v -race ./...` — all tests pass with zero races
- [ ] Profile with `go test -bench=. -benchmem -cpuprofile cpu.out ./...` and view with `go tool pprof cpu.out`
- [ ] Journal: weekly retrospective — which concurrency pattern do you feel most confident with? Which still feels uncertain?

---

## Resources

- [Go Blog — Pipelines and Cancellation](https://go.dev/blog/pipelines)
- [Go Blog — Contexts and structs](https://go.dev/blog/context-and-structs)
- [sync package docs](https://pkg.go.dev/sync)
- [context package docs](https://pkg.go.dev/context)
- [Go by Example — Worker Pools](https://gobyexample.com/worker-pools)
