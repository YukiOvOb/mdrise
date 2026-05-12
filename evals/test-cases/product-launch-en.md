# Glimpse

**Stream-aware JSON visualization for your terminal.**

Glimpse turns the firehose of structured logs and event streams into something a human can actually parse — without leaving the terminal.

---

## Why we built this

If you've ever piped `kubectl logs -f` into `jq` and immediately regretted it, this is for you.

JSON logs are great for machines and miserable for humans. `jq` formats one record at a time. Your terminal becomes a wall of green. You're three minutes into an outage and you can't find the field you need.

Glimpse stays out of your way until you need it — then folds, filters, colors, and reshapes the stream live.

## Features

- **Live folding.** Collapse any path in real time. The stream keeps flowing.
- **Schema-aware coloring.** Glimpse learns your fields after ~50 records and assigns stable colors so `error.code` always looks the same.
- **Stateful filters.** Filter expressions persist across reconnects. `level=error AND service=auth-*` survives a pod restart.
- **Replay buffer.** Last 10 MB of stream kept in memory. Scroll back without re-running the command.
- **One binary.** Static Go binary, no runtime, no dependencies, ~6 MB.

## Quick start

```bash
# install
brew install glimpse-stream/tap/glimpse

# pipe in any JSON stream
kubectl logs -f deploy/api -n prod | glimpse

# with a saved filter
glimpse --filter "level >= warn" --color-by service
```

Press `/` to filter, `f` to fold, `?` for everything else.

## How it compares

| Tool        | Live | Stateful filters | Schema coloring | Replay |
|-------------|:----:|:----------------:|:---------------:|:------:|
| `jq`        |  -   |        -         |        -        |   -    |
| `fblog`     |  ✓   |        -         |        -        |   -    |
| `lnav`      |  ✓   |        ✓         |        -        |   ✓    |
| **Glimpse** |  ✓   |        ✓         |        ✓        |   ✓    |

## Status

Glimpse is at **0.4** — used daily by the maintainers, breaking changes still possible. v1.0 in Q3 2025 when the filter DSL stabilizes.

## License

MIT. See [LICENSE](LICENSE).

> Built by people who got paged at 3 AM one too many times.
