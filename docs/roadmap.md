# Roadmap

Each step ends with something you can run.

| # | Step | Done when | Main concepts |
|---|------|-----------|---------------|
| 0 | CLI skeleton: `clap` with `listen` / `call`, `anyhow` | `bak-bak --help` shows both subcommands | Cargo, modules, `Result` and `?`, enums |
| 1 | Two iroh endpoints, connect by ticket, `ping` / `pong` over a bi-stream | `call` prints `pong` | async/await, tokio runtime, iroh `Endpoint`, ALPN, tickets, QUIC streams |
| 2 | Text chat both ways; clean exit on Ctrl-C or peer hang-up | Both sides type and read at once; no hung tasks on exit | `tokio::spawn`, `select!`, channels, `Send + 'static`, cancellation, framing |
| 3 | Mic to speakers locally with `cpal`, no network | You hear yourself with low delay and no crackle | real-time callbacks, threads vs tasks, ring buffers, sample formats |
| 4 | Raw PCM over an iroh stream | You hear the other peer | bridging sync audio and async network, backpressure, byte encoding |
| 5 | Opus encode/decode | Measured bandwidth before and after | FFI-backed crates, frame sizes, bitrate, traits for a swappable codec |
| 6 | QUIC datagrams plus a jitter buffer | Audio survives simulated loss and jitter | unreliable delivery, sequence numbers, reordering, loss concealment |
| 7 | Stretch: push-to-talk, more than two peers, TUI (`ratatui`) | — | raw mode, state machines, fan-out, mixing |
