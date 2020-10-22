+++
title = "Installation"
weight = 2
+++

## Common steps

First, [install docker](https://docs.docker.com/install/), if you haven't
already.

## Install in Linux

You can install Avatar-CLI in two different ways:
- Via [pre-compiled binaries](@/documentation/installation.md#via-pre-compiled-binaries)
- Via [Cargo](@/documentation/installation.md#via-cargo)

## Install in Macos

For now there's only one way to install Avatar-CLI in Macos:
- Via [Cargo](@/documentation/installation.md#via-cargo)

## Via pre-compiled binaries

For now, only Linux binaries are available.

1. Download a pre-compiled binary from the
   [Releases](https://gitlab.com/avatar-cli/avatar-cli/-/releases) section.
2. Place the file in a directory listed in the `$PATH` environment variable,
   like `/usr/bin`, or `$HOME/.local/bin`.
3. Make it executable with `chmod +x /path/to/avatar` (adapt the path to your
   particular case).

## Via Cargo

If you are a [Rust](https://www.rust-lang.org/) developer, then you already know
[Cargo](https://doc.rust-lang.org/cargo/). If you don't have it in your system
then you can obtain it via [rustup](https://rustup.rs/).

Once you have cargo, you can install Avatar-CLI with the following command:

```sh
cargo install avatar-cli
```
