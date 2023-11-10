# Fly Minecraft

A tiny project for deploying Minecraft to Fly.io.

## Roll-out

### Preparation

First things first, _setup the WHITELIST env var_ in the `fly.toml`. This should
be the Minecraft usernames you want to grant access to the server. Be sure to
include your Minecraft username for testing.

Also add your Minecraft username to the `OPS` env var. These are server
administrators.

### Execution

First decide on a globally unique Fly app name, and assign it to a an env var.
Then create necessary resources in Fly with the script below.

When running the `fly deploy` command below, be sure to follow the prompt to
allocate dedicated ipv4 and ipv6 addresses.

```bash
export UNIQUE_NAME="ckreiling" # replace with your unique name
fly apps create minecraft-$UNIQUE_NAME
fly volumes create -a minecraft-$UNIQUE_NAME minecraft_data
fly deploy -a minecraft-$UNIQUE_NAME \
  --vm-size shared-cpu-4x \
  --vm-memory 4096
```

Shortly after roll-out, you should be able to connect directly to
`minecraft-$UNIQUE_NAME.fly.dev` via the Minecraft client.

## Destruction

Destroying the Minecraft server is easy:

```bash
fly apps delete minecraft-$UNIQUE_NAME
```
