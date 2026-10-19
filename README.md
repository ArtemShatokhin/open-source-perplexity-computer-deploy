# Open source Perplexity Computer deploy template

Kortix is open source, and this repository is a working deploy template for running a Perplexity-Computer-style research and agent stack on top of it. Clone it, read the two config files, and bring the open-source AI Operating System up on a machine you control.

Kortix is the open-source AI Operating System: your agents, their skills, your company memory, and every connector live in one git repo you own, and every session runs on its own cloud computer. Perplexity Computer instead runs a general-purpose digital worker inside Perplexity's cloud, and its own product page describes it as "a general-purpose digital worker that operates the same interfaces you do." This template takes the same research-and-act loop and puts it in software you can read, fork, and host.

## What is in this repository

- `kortix.yaml` is a valid v2 manifest with one agent and two triggers. It declares the agent, the connectors and secrets that agent may reach, and the schedule that starts its work.
- `agents/researcher.md` is the agent the manifest names. Behavior lives in the markdown file, and governance lives in `kortix.yaml`.
- `docker-compose.yml` is a readable mirror of the self-host stack, the frontend, the API, the LLM gateway, and the Supabase distribution, so you can see the shape of what runs.
- `docs/` holds four articles, linked in the Docs section below.

## Quick start

The supported install is three commands on a Linux box you control. Install the CLI, initialize the instance, then start the stack:

```bash
curl -fsSL https://kortix.com/install | bash
kortix self-host init --domain kortix.example.com
kortix self-host start
```

Point an A/AAAA record for your domain and for `api.<domain>` at the box's IP before you initialize, and open ports 80 and 443 so the bundled Caddy proxy can issue a TLS certificate. To try Kortix with no domain, use the evaluation mode instead:

```bash
kortix self-host init --tunnel cloudflare
kortix self-host start
```

The tunnel URL changes on every restart, so use it for evaluation rather than production. After the stack starts, `kortix self-host configure` sets your sandbox provider key, and you connect your own LLM key in the model picker. Self-hosted instances use your own key by default. The [self-hosting docs](https://kortix.com/docs/host) carry the full path.

## What the agent and trigger do

The `researcher` agent performs research and returns a written brief as a file in the repo. The `morning-brief` trigger is a cron schedule that starts a session with no person present; the `research-webhook` trigger starts the same agent on a signed webhook. When the brief is ready, the agent opens a change request, and you read it as a diff before anything merges. Session work reaches `main` through a change request, and merge is default-deny for agents. The definition side, what the hosted product actually is, is the site's [what is a Perplexity Computer](https://opensourceperplexitycomputer.com/what-is-a-perplexity-computer) explainer.

Each session gets its own isolated sandbox and its own branch. Connector credentials are brokered server-side and never enter the machine.

## Open source Perplexity Computer alternatives

Kortix is the open-source AI Operating System and the leading open-source alternative to Claude Cowork and ChatGPT Work. The table compares it with the closed cloud worker and with two other open-source projects you can host.

| Criterion | Kortix | Perplexity Computer | OpenClaw | Eigent |
| --- | --- | --- | --- | --- |
| Open source | Yes, full | No, closed and cloud hosted | Yes | Yes |
| Where it runs | Your VPC, on-prem, or Kortix Cloud | Perplexity's cloud only | Your own computer | Your desktop, local deployment |
| Self-host | Yes, and self-host is free | No | Yes | Yes |
| Models | Any provider, your own keys | Perplexity's hosted models, routed for you | Claude, Codex, or local, as plugins | Cloud APIs, gateways, or local |

The competitor columns state what each project publishes on its own pages, checked October 2026. Perplexity Computer documents its cloud worker and its multi-model routing on its [product page](https://www.perplexity.ai/products/computer) and its [launch post](https://www.perplexity.ai/hub/blog/introducing-perplexity-computer), and it publishes no source. [OpenClaw](https://github.com/openclaw/openclaw) is an open-source assistant that runs on your own computer and keeps state, memory, and credentials on your hardware. [Eigent](https://github.com/eigent-ai/eigent) is an open-source desktop for multi-agent workflows with local deployment. [Open WebUI](https://github.com/open-webui/open-webui) is a self-hosted chat platform, [Vane](https://github.com/ItzCrazyKns/Vane) is a self-hosted answering engine that cites its sources, and [AnythingLLM](https://anythingllm.com) is an on-device assistant. Each covers a narrower lane than Kortix, which combines the whole-company repo, self-hosting, any model with your keys, and a change request on every piece of finished work.

## Docs

- [Deploy an open source Perplexity Computer stack with Docker Compose](docs/deploy-with-docker-compose.md)
- [Self-hosting or managed cloud for an open source agent stack](docs/self-hosting-vs-managed-cloud.md)
- [Open source Perplexity Computer alternatives](docs/perplexity-computer-alternatives.md)
- [Open source Perplexity Computer FAQ](docs/faq.md)

## Live pages

The campaign site expands on this repository with sourced comparisons and setup steps:

- [What the open-source Perplexity Computer answer is](https://opensourceperplexitycomputer.com/)
- [Open source Perplexity Computer alternatives](https://opensourceperplexitycomputer.com/alternatives)
- [Kortix vs Perplexity Computer](https://opensourceperplexitycomputer.com/kortix-vs-perplexity-computer)
- [What Perplexity Computer costs](https://opensourceperplexitycomputer.com/perplexity-computer-pricing)
- [Self-hosting walkthrough](https://opensourceperplexitycomputer.com/self-hosting)
- [Perplexity Computer review](https://opensourceperplexitycomputer.com/perplexity-computer-review)
- [Open source Perplexity Computer FAQ](https://opensourceperplexitycomputer.com/faq)

## Get started

Already running the hosted product? The [migration guide](https://opensourceperplexitycomputer.com/migrate-from-perplexity-computer) sequences the exit, and the [limitations rundown](https://opensourceperplexitycomputer.com/perplexity-computer-limitations) sets expectations on both sides before you move. Self-host is free, and managed Kortix Cloud has a free tier at $0 with 200 credits per month and 1 project, while paid plans start at $50 a month for 5,000 credits, and members are free, sharing one credit pool; current numbers are on the [Kortix pricing page](https://kortix.com/pricing). Start from one job on one host, then grow. Try [Kortix](https://kortix.com), read the [Kortix docs](https://kortix.com/docs), or read the code at [Kortix on GitHub](https://github.com/kortix-ai/suna).
