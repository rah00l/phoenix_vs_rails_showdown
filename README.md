# Benchmarking Phoenix vs Rails (WIP)

Machine: MacBook Pro Intel Core i7 (2.7 GHz 4 Cores) 16 GB RAM

## Benchmarking Phoenix
Elixir 0.14.2

```bash
$ mix do deps.get, compile
$ MIX_ENV=prod mix compile.protocols
$ MIX_ENV=prod elixir -pa _build/prod/consolidated -S mix phoenix.start
Running Elixir.Benchmarker.Router with Cowboy on port 4000

$ wrk -t4 -c100 -d30S --timeout 2000 "http://127.0.0.1:4000/showdown"
Running 30s test @ http://127.0.0.1:4000/showdown
  4 threads and 100 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency     4.80ms    2.18ms  54.70ms   98.36%
    Req/Sec     5.61k   755.82     8.00k    71.80%
  639868 requests in 30.00s, 1.31GB read
Requests/sec:  21329.21
Transfer/sec:     44.75MB
```

## Benchmarking Rails
MRI 2.1.2

```bash
$ bundle
$ PUMA_WORKERS=4 MIN_THREADS=1 MAX_THREADS=16 RACK_ENV=production bundle exec puma
[51026] Puma starting in cluster mode...
[51026] * Version 2.8.2 (ruby 2.1.2-p95), codename: Sir Edmund Percival Hillary
[51026] * Min threads: 1, max threads: 16
[51026] * Environment: production
[51026] * Process workers: 4
[51026] * Preloading application
[51026] * Listening on tcp://0.0.0.0:3000
[51026] Use Ctrl-C to stop
[51027] + Gemfile in context: /Users/goyox86/Code/phoenix_vs_rails_showdown/rails/benchmarker/Gemfile
[51028] + Gemfile in context: /Users/goyox86/Code/phoenix_vs_rails_showdown/rails/benchmarker/Gemfile
[51026] - Worker 0 (pid: 51027) booted, phase: 0
[51029] + Gemfile in context: /Users/goyox86/Code/phoenix_vs_rails_showdown/rails/benchmarker/Gemfile
[51026] - Worker 1 (pid: 51028) booted, phase: 0
[51026] - Worker 2 (pid: 51029) booted, phase: 0
[51030] + Gemfile in context: /Users/goyox86/Code/phoenix_vs_rails_showdown/rails/benchmarker/Gemfile
[51026] - Worker 3 (pid: 51030) booted, phase: 0

$ wrk -t4 -c100 -d30S --timeout 2000 "http://127.0.0.1:3000/showdown"
Running 30s test @ http://127.0.0.1:3000/showdown
  4 threads and 100 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency    29.48ms   12.55ms 125.61ms   72.21%
    Req/Sec   493.61    150.85   800.00     57.17%
  57720 requests in 30.00s, 128.95MB read
Requests/sec:   1923.86
Transfer/sec:      4.30MB
```


