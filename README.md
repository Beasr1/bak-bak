# bak-bak

A peer-to-peer walkie-talkie for the terminal, written in Rust on [iroh](https://iroh.computer).

One person listens and gets a ticket. The other calls with that ticket. Voice goes over a direct, encrypted QUIC connection between the two machines, with no server in the middle.

```sh
bak-bak listen            # prints a ticket
bak-bak call <ticket>     # connects and starts talking
```

> **Status:** early. Built step by step as a way to learn Rust, iroh and real-time audio. The commands above are the goal, not the current state.

## Roadmap

- [ ] CLI skeleton (`listen`, `call`)
- [ ] Connect two endpoints by ticket; ping/pong over a stream
- [ ] Two-way text chat
- [ ] Local mic-to-speaker loopback
- [ ] Raw audio over the network
- [ ] Opus compression
- [ ] Datagrams with a jitter buffer
- [ ] Push-to-talk, group calls, TUI

## Requirements

- Rust (stable), via [rustup](https://rustup.rs)
- libopus, from the Opus step onward: `brew install opus` on macOS
- On macOS, give your terminal app microphone access: System Settings > Privacy & Security > Microphone

## Building

```sh
cargo build --release
```

## Docs

- [Roadmap](docs/roadmap.md)
- [Architecture](docs/architecture.md)
- [Development](docs/development.md)

## Acknowledgements

- [iroh](https://github.com/n0-computer/iroh) for direct peer-to-peer connections
- [callme](https://github.com/n0-computer/callme), n0's own voice-call demo on iroh
