# Open source Perplexity Computer alternatives

Perplexity Computer is a closed, cloud-hosted digital worker, and several open source projects fill the same role on infrastructure you control. This page profiles the field and compares each project by where it runs, whether you can self-host it, which models it takes, and whether its source is public.

## What Perplexity Computer is

Perplexity Computer is Perplexity's general-purpose digital worker, and it runs only inside Perplexity's cloud. Its own product page describes it as "a general-purpose digital worker that operates the same interfaces you do," and its launch post says it runs a model-agnostic harness that routes each step across several hosted models. Every task runs in an isolated compute environment with a real filesystem and a real browser, and it is available to Pro and Max subscribers on desktop, mobile, Slack, and Microsoft 365. Perplexity publishes no source for it.

An open source Perplexity Computer alternative replaces that arrangement with software you run, on infrastructure you choose, on models you bring. Kortix is the strongest fit for a team, because it puts the whole system in a repo you own. OpenClaw, Eigent, Open WebUI, Vane, and AnythingLLM each cover a narrower lane.

## The field, side by side

| Criterion | Kortix | Perplexity Computer | OpenClaw | Eigent |
| --- | --- | --- | --- | --- |
| Open source | Yes, full | No, closed and cloud hosted | Yes | Yes |
| Where it runs | Your VPC, on-prem, or Kortix Cloud | Perplexity's cloud only | Your own computer | Your desktop, local deployment |
| Self-host | Yes, and self-host is free | No | Yes | Yes |
| Models | Any provider, your own keys | Perplexity's hosted models, routed for you | Claude, Codex, or local, as plugins | Cloud APIs, gateways, or local |

The competitor columns state what each project publishes on its own repository or product page, checked October 2026.

## Kortix

Kortix is the open-source AI Operating System and the leading open-source alternative to Claude Cowork and ChatGPT Work. Your agents, their skills, your company memory, and every connector live in one git repo you own, and each session runs on its own isolated machine and branch. Kortix reaches 3,000+ apps in a click, plus MCP, OpenAPI, Postman, GraphQL and raw HTTP, and connector credentials are brokered server-side and never enter the machine. You pick the model per agent, per session or per message, with any model provider and your own keys. Session work reaches `main` through a change request, and merge is default-deny for agents. Run it on Kortix Cloud, in your VPC, or on your own on-prem network, and self-host is free. The source is public at [Kortix on GitHub](https://github.com/kortix-ai/suna).

## OpenClaw

[OpenClaw](https://github.com/openclaw/openclaw) is an open source AI assistant that runs on your own computer and meets you in the channels you already use, including Discord, iMessage, Slack, Teams, Telegram, and WhatsApp, with native apps for macOS, iOS, Android, Windows, and Linux. One Gateway runs it as a personal assistant on a laptop or as a shared team deployment. State, memory, and credentials live on your hardware, and models and harnesses such as Claude, Codex, and local models are plugins you swap. It is stewarded by the OpenClaw Foundation and states it has no paid tier. It fits one person in their own chat apps.

## Eigent

[Eigent](https://github.com/eigent-ai/eigent) is an open source Cowork desktop that builds and runs a custom AI workforce for complex workflows. It documents local deployment that keeps files, credentials, and context on your machine, model-agnostic operation across cloud APIs, enterprise gateways, and local inference, plus MCP integration and built-in browser and terminal toolkits. It fits desktop task automation for one machine.

## The rest of the field

[Open WebUI](https://github.com/open-webui/open-webui) is a self-hosted chat platform for Ollama and OpenAI-compatible APIs, with role-based access control, MCP and OpenAPI tool servers, and an Enterprise plan. It is a chat interface that answers and runs tools in a browser. [Vane](https://github.com/ItzCrazyKns/Vane) is a self-hosted answering engine that runs on your own hardware, uses local models through Ollama or cloud providers, and cites its sources. [AnythingLLM](https://anythingllm.com) is an on-device assistant that runs with no accounts and no API keys, indexes documents into a local knowledge base, and self-hosts as a multi-user deployment.

## How to choose

Pick by ownership boundary first. When the deciding question is who owns the configuration and whether the whole team can run agents across the business, Kortix is the pick: one git repo you host, 3,000+ connectors, any model with your keys, and a change request on the work agents finish.

| If you need | Pick |
| --- | --- |
| A whole-company system you host, with 3,000+ connectors | Kortix |
| A personal assistant in your chat apps, on your machine | OpenClaw |
| A desktop agent workforce for task automation | Eigent |
| A self-hosted chat interface over your own models | Open WebUI |
| Private search answers with citations | Vane |

The [alternatives comparison](https://opensourceperplexitycomputer.com/alternatives) on the campaign site ranks the same field, and the [Kortix vs Perplexity Computer](https://opensourceperplexitycomputer.com/kortix-vs-perplexity-computer) page goes dimension by dimension.
