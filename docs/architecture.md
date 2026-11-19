# Architecture

> Proposed layout. It will change as the code is written; update this file when it does.

## Overview

```
 mic ──▶ capture ──▶ encode ──▶ send ═══ QUIC (iroh) ═══▶ receive ──▶ jitter buffer ──▶ decode ──▶ playback ──▶ speakers
        (cpal thread)                (async tasks)                     (async)                    (cpal thread)
```

Each peer runs both directions at once. Audio devices run on real-time OS threads owned by cpal. Networking runs on tokio tasks. The two meet only through lock-free buffers or channels, so the audio threads never wait on the network.

## Package layout

A single package with a library and a thin binary, so the logic can be tested from `tests/`.

```
src/
  main.rs          CLI parsing only; calls into the library
  lib.rs           declares modules
  cli.rs           clap types (Listen, Call { ticket })
  net.rs           endpoint setup, ALPN constant, ticket encode/decode, accept/connect
  proto.rs         wire format: message types, framing, datagram header
  chat.rs          text session (step 2)
  audio/
    mod.rs
    device.rs      cpal input/output streams
    codec.rs       Encoder/Decoder traits; PCM and Opus implementations
    jitter.rs      jitter buffer
  session.rs       wires net and audio together; owns the tasks
```

## Boundaries

| Module | Knows about | Must not know about |
|--------|-------------|---------------------|
| `audio/` | samples, devices, codecs | iroh, sockets |
| `net.rs` | iroh, connections, tickets | audio |
| `proto.rs`, `audio/jitter.rs` | bytes, sequence numbers, time | any I/O (so they are unit-testable) |
| `session.rs` | everything | — (the only place they meet) |

## Protocol

To be written in `docs/protocol.md` once the wire format exists: the ALPN string, stream and datagram usage, the framing, and the datagram header (sequence number, timestamp).
