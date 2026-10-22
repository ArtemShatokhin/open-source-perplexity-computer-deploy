# Deploy an open source Perplexity Computer stack with Docker Compose

Kortix is the open-source AI Operating System, and it self-hosts as one Docker Compose stack: the frontend, the API, the LLM gateway, and the Supabase distribution. This guide walks through the documented install paths, the commands each one runs, and the data you back up.

## What the stack runs

A Kortix instance is a single Docker Compose stack. The frontend serves the dashboard, the API holds project state and serves the public `/v1` routes, and the LLM gateway authenticates model-provider requests server-side. A Supabase distribution provides the database, auth, storage, and the object store the API archives config into. The bundled Caddy proxy terminates TLS on ports 80 and 443.

Agent sessions do not run in this stack. Each session runs on a separate sandbox provider, so a laptop-sized host can run the control plane while the agents work on cloud machines. Platinum is the default provider, and Daytona remains available as a legacy fallback. You set the provider key with `kortix self-host configure`.

## Install the CLI and initialize

The supported path is three commands on a Linux box you control. Install the CLI, initialize the instance, then start the stack:

```bash
curl -fsSL https://kortix.com/install | bash
kortix self-host init --domain kortix.example.com
kortix self-host start
```

Before you run `init`, create an A/AAAA record for your domain and for `api.<domain>`, both pointing at the box's IP, and open ports 80 and 443 so Caddy can issue a TLS certificate. Check progress with `kortix self-host status`, `kortix self-host logs`, and `kortix self-host doctor` while the stack starts.

On a bare Linux box, a one-shot bootstrap script installs Docker, installs the CLI, and starts the stack in one command. It runs on Linux only, and the [self-hosting docs](https://kortix.com/docs/host) carry the exact invocation alongside the manual path above.

## Evaluation mode with no domain

To try Kortix with no domain, use a Cloudflare tunnel instead:

```bash
kortix self-host init --tunnel cloudflare
kortix self-host start
```

The tunnel URL changes on every restart, so treat this mode as an evaluation path, not production. The instance still needs outbound internet access, because `kortix self-host start` pulls images from docker.io and the sandbox must be able to call back to the API.

## Connect models and set limits

After the stack starts, `kortix self-host configure` asks for the sandbox provider key and, optionally, a managed-git token. Connect your own LLM key in the model picker. Self-hosted instances use your own key by default, and the model is chosen per agent, per session or per message.

Each API container has a 640 MiB memory limit by default. Keep that default on an 8 GiB host; on a 16 GiB host, raise it when API traffic reaches the limit:

```bash
kortix self-host env set KORTIX_API_MEMORY_LIMIT=1024m
```

Confirm the applied limit with `docker stats --no-stream`.

## Updates and backups

Every instance updates itself automatically. Pin an exact version with `kortix self-host update --tag 0.9.84`, or turn the updater off with `--auto-update off`.

Kortix has no separate backup system. Each instance stores its data in two directories under `~/.config/kortix/self-host/<instance>/`: `volumes/db/data` holds the Postgres database, and `volumes/storage` holds file storage. The instance `.env` file holds every secret and signing key it uses. Back up all three before you run a destructive command.

The [self-hosting docs](https://kortix.com/docs/host) carry the full reference, including the architecture page and every `kortix self-host` subcommand.
