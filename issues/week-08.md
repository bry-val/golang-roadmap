**Title:** Week 8: Standard Library HTTP & JSON — Apr 13–17  
**Labels:** `phase-1`, `week-8`  
**Milestone:** Phase 1 — Go Foundations  
**Assignee:** @bry-val

---

## Goal

Build a fully functional JSON REST API using only the Go standard library — no frameworks — to internalise routing, middleware, request/response handling, and JSON serialisation.

---

## Monday, Apr 13 — `net/http` Server Basics

- [ ] Write the smallest possible HTTP server: `http.HandleFunc("/", ...)` + `http.ListenAndServe(":8080", nil)`
- [ ] Define a custom `ServeMux` (not `DefaultServeMux`) and register multiple routes
- [ ] Implement a `Handler` struct with a `ServeHTTP(w http.ResponseWriter, r *http.Request)` method
- [ ] Return proper status codes: `http.StatusOK`, `http.StatusNotFound`, `http.StatusMethodNotAllowed`
- [ ] Set response headers: `w.Header().Set("Content-Type", "application/json")`
- [ ] Read request headers and query parameters: `r.Header.Get(...)`, `r.URL.Query().Get(...)`
- [ ] Read: [net/http package docs](https://pkg.go.dev/net/http) — skim `Handler`, `HandlerFunc`, `ServeMux`, `ResponseWriter`, `Request`
- [ ] Journal: what is the difference between `http.Handle` and `http.HandleFunc`?

## Tuesday, Apr 14 — `encoding/json`

- [ ] Marshal a struct to JSON with `json.Marshal` and pretty-print with `json.MarshalIndent`
- [ ] Add struct tags: `json:"field_name"`, `json:",omitempty"`, `json:"-"` (excluded) — observe effects
- [ ] Unmarshal a JSON string into a struct with `json.Unmarshal`; handle a malformed JSON error
- [ ] Use `json.Decoder` to stream-decode a large JSON array from an `io.Reader` (e.g. `strings.NewReader`)
- [ ] Use `json.Encoder` to stream-encode to `http.ResponseWriter` directly
- [ ] Marshal a `map[string]any` and unmarshal JSON into `map[string]any`; compare to typed struct approach
- [ ] Write a helper `WriteJSON(w http.ResponseWriter, status int, v any) error` that encodes and sets headers
- [ ] Journal: when would you choose `json.Decoder` over `json.Unmarshal`?

## Wednesday, Apr 15 — `net/http` Client

- [ ] Make a GET request with `http.Get(url)` and read the response body safely (always close with `defer resp.Body.Close()`)
- [ ] Make a POST request with `http.NewRequestWithContext`, set JSON body and `Content-Type` header
- [ ] Set a client-level timeout: `client := &http.Client{Timeout: 5 * time.Second}`
- [ ] Inspect response status codes and handle `4xx`/`5xx` as errors
- [ ] Set custom request headers (e.g. `Authorization: Bearer <token>`)
- [ ] Use `httptest.NewServer` to create a test server and point your client at it in tests
- [ ] Journal: why should you always set a timeout on `http.Client`, and what happens if you don't?

## Thursday, Apr 16 — Middleware Pattern & Structured Logging

- [ ] Define a middleware type: `type Middleware func(http.Handler) http.Handler`
- [ ] Write a `Logger` middleware that prints method, path, status code, and duration for every request
- [ ] Write a `Recoverer` middleware that catches panics, returns `500`, and logs the stack trace
- [ ] Write an `Auth` middleware that checks for a `Bearer` token in the `Authorization` header; return `401` if missing
- [ ] Chain middlewares with a `Chain(h http.Handler, mws ...Middleware) http.Handler` helper
- [ ] Add `log/slog` structured logging (Go 1.21+) — log key-value pairs instead of raw strings
- [ ] Journal: why is middleware preferred over putting cross-cutting logic inside handlers?

## Friday, Apr 17 — Mini-Project: In-Memory REST API

- [ ] Implement a `/api/items` resource with `GET` (list), `POST` (create), `GET /api/items/{id}` (read), `PUT /api/items/{id}` (update), `DELETE /api/items/{id}` (delete)
- [ ] Store items in an in-memory `map[string]*Item` protected by a `sync.RWMutex`
- [ ] Parse path parameters manually from `r.URL.Path` (no router library)
- [ ] Apply the Logger, Recoverer, and Auth middleware chain to all routes
- [ ] Write integration tests using `httptest.NewRecorder` and `httptest.NewServer` for all five endpoints
- [ ] Test error cases: missing item (404), bad JSON body (400), missing auth token (401)
- [ ] Run `go test -v -race ./...` — all tests pass with zero races
- [ ] Journal: weekly retrospective — what would you change if you could use one external library? Why?

---

## Resources

- [net/http package docs](https://pkg.go.dev/net/http)
- [encoding/json package docs](https://pkg.go.dev/encoding/json)
- [Go by Example — HTTP Server](https://gobyexample.com/http-server)
- [Go by Example — HTTP Client](https://gobyexample.com/http-client)
- [Go by Example — JSON](https://gobyexample.com/json)
- [Effective Go — The http package](https://pkg.go.dev/net/http)

---

## 🎉 Phase 1 Complete!

Finishing Week 8 means you have:

- A solid command of Go syntax, types, and idioms
- Concurrency tools (goroutines, channels, sync, context) in your toolkit
- A professional testing practice (table-driven, benchmarks, coverage, mocks)
- A working HTTP + JSON foundation for backend services

**Next up — Phase 2:** Databases, gRPC, Docker, and production-ready backend patterns.
