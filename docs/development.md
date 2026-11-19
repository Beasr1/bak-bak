# Development

## Setup (macOS)

```sh
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh   # Rust toolchain
brew install opus                                                # needed from the Opus step onward
```

Give your terminal app (Terminal, iTerm, VS Code) microphone access: System Settings > Privacy & Security > Microphone.

## Everyday commands

```sh
cargo run -- listen
cargo run -- call <ticket>
cargo test
cargo clippy --all-targets
cargo fmt
```

To try it on one machine, run `listen` and `call` in two terminals. Use headphones once audio crosses the network, or the speakers will feed back into the mic.

## Simulating a bad network

The jitter buffer step needs loss and delay to test against. On macOS, Apple's Network Link Conditioner (in Xcode's Additional Tools download) can add both.

## Commits

- Style: `type(scope): message`, for example `feat(net): connect two endpoints by ticket`.
- Use the personal Gmail identity. Run `./.gitsafety` before committing to check `git config user.email`.

## References

- iroh: https://docs.iroh.computer, https://docs.rs/iroh
- tokio: https://tokio.rs/tokio/tutorial
- cpal: https://docs.rs/cpal
- Opus bindings: https://docs.rs/opus, https://docs.rs/audiopus
- callme (n0's voice demo on iroh, for reading): https://github.com/n0-computer/callme
