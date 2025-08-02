## Server share

Utility to share your local server without public IP address. Built with [iroh](https://crates.io/crates/iroh) library which uses [QUIC](https://en.wikipedia.org/wiki/QUIC) [peer-to-peer](https://en.wikipedia.org/wiki/Peer-to-peer) [holepunching](https://en.wikipedia.org/wiki/Hole_punching_(networking)).


### Installation

1. You need Rust Programming Language, install it from https://www.rust-lang.org/tools/install
2. In terminal run:
    ```bash
    cargo install --git https://github.com/Kazik24/server_share.git
    ```
    This will compile and install `server_share` binary to use from your terminal (it may take few minutes).

### Usage

**Starting server:**

To enable other users to connect yo your locally running server, open terminal on machine with your server and run:

```bash
server_share serve localhost:25565
```
This will display a ticket that can be used by other users to connect to your locally running server:
```
Use this ticket to connect: sp2p4zvwRjXUKGfvwnParsHAS3HuSVzV5cA4McphgmoCtajS
```

**Connecting to server:**

To connect to your locally running server from different computer, open terminal on other machine and run:

```bash
server_share listen --from localhost:25565 sp2p4zvwRjXUKGfvwnParsHAS3HuSVzV5cA4McphgmoCtajS
```
This will listen on port 25565 (you can specify other port or bind address) and forward all connections from this port to server running at
the first machine with given ticket.

**Making ticket persistent:**

Sometimes you want to keep your server ticket stable, for example to not reshare it with other users every time you start your server.
To make your ticket persistent, generate a config.toml file with your secret key by running command:

```bash
server_share prepare
```
This will generate a config.toml file in current directory that will look like this:
```toml
[config]
secret_key = "11111111111111111111111111111111" # of course you will have a different key here every time you run this command
```
After that you can run `server_share serve ...` and it will present you the same ticket every time.
