# Logger

Logger is a very simple and fast logger that can write both machine-readable and human-readable logs.

### Why?

I made logger because I really liked zerolog, and especially its `ConsoleLogger`, as it looks really nice in the terminal. I use it in all my command-line applications, but there's an issue. Zerolog can only output in JSON or CBOR, depending on buid tags. It cannot produce human-readable output. Therefore, zerolog has to use reflection to unmarshal JSON generated by the logger and then make human-readable output out of it. This is, in my opinion, incredibly and unnecessarily wasteful, so I made logger. Logger can use any logging implementation that implements the `logger.Logger` interface. I currently have four implementations: `JSONLogger`, `PrettyLogger`, `MultiLogger`, and `NopLogger`. The names should be self-explanatory.

### Who is logger for?

If you need a fast and simple logger, but don't need more advanced features such as context and hooks, logger is for you. It cuts out unnecessary features, providing a very simple codebase that is easy to test and has much less potential for bugs, and it's faster than zerolog while also allowing more flexibility and a similar API.

### Who is logger not for?

If you need more advanced features, such as context and hooks, use either zerolog or the even faster zap library. Logger keeps it as simple as possible, only providing logging and nothing else.

### Benchmarks

Logger is very fast. Here are its benchmarks, done on my laptop:

```text
goos: linux
goarch: amd64
pkg: logger
cpu: 11th Gen Intel(R) Core(TM) i7-1185G7 @ 3.00GHz
BenchmarkJSON/one-field-8                4216245               294.0 ns/op           160 B/op          3 allocs/op
BenchmarkJSON/two-field-8                1939634               594.3 ns/op           188 B/op          5 allocs/op
BenchmarkJSON/all-8                       310526              3955 ns/op             752 B/op         21 allocs/op
BenchmarkPretty/one-field-8              1603789               658.5 ns/op           168 B/op          4 allocs/op
BenchmarkPretty/two-field-8              1388920               864.5 ns/op           200 B/op          6 allocs/op
BenchmarkPretty/all-8                     285554              3726 ns/op             760 B/op         22 allocs/op
```

To run the benchmarks yourself, simply clone this repo and run `go test -bench=.`. Keep in mind that they will be different, depending on what your computer's specs are.
