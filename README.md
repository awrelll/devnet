# OpenLibra Devnet

Coordination repository for the OpenLibra Devnet.

We are ready to start registering nodes for the initial OpenLibra Devnet.
Follow the instructions below to generate your node keys and commit them
to this repository.

## How to Join

To join the Devnet, you'll need to do the following

- Install Rust: <https://rustup.rs/>
  - Note: make sure to `source ~/.cargo/env` when you're done
- Clone this repository:
  - `git clone https://github.com/open-libra/devnet`
- Initialize git submodules:
  - `git submodule update --init`
- Build the [OpenLibra CLI][1] utility. From the root of this repo:
  - `cargo install --locked --path cli`
- Generate your node keys and `peer_info.toml` (see section below)
- Fork this GitHub repository and commit your `peer_info.toml`
- [Clone and Build Libra Core][2]
- After enrollment is closed, we will generate `genesis.blob` and other
  configuration files you can use to join the Devnet.

## Generating Validator Config and Keys

After installing the OpenLibra CLI, you can generate node keys by running
the following:

```
$ open-libra config -a 1.2.3.4 -o my-node-config
```

The `open-libra config` command accepts the following arguments:

- `-a`: public IP address to advertise to the network. This is the public IPv4
        address of your validator node.
- `-o`: output path where config should be placed. If the directory doesn't
        exist, it will be created automatically.
- `-s`: (or `--seed`, optional): include this validator in the Devnet's global
        list of seed nodes. Only add this option if you plan to run a highly
        available validator node with a static IP address.

This command will generate a number of files in the `my-node-config`:

- `node.config.toml`: main node configuration file
- `consensus_keypair.config.toml`: validator consensus keys
- `network_keypairs.config.toml`: network peer identity keys
- `peer_info.toml`: public peer information - open a PR with this to join the devnet

## Opening a PR with `peer_info.toml`

- (Optional) edit the file and set `description`, `website_url`, and `logo_url`
  for your node.
- Rename the `peer_info.toml` file to `mynodename.peer_info.toml`
- Place it in the `devnet-0/peer_info_files` directory to this repo
- Commit the file to this repo
- Open a PR to https://github.com/open-libra/devnet

[//]: # (links)

[1]: https://github.com/open-libra/cli
[2]: https://developers.libra.org/docs/my-first-transaction#clone-and-build-libra-core
