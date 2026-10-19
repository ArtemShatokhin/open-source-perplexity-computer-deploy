# Open source Perplexity Computer stack: FAQ

Kortix is open source, and this FAQ answers the questions a team asks before it replaces a hosted cloud worker with a stack it runs. Each answer stands on its own, with the primary source linked where a claim would otherwise be hard to check.

## Is Perplexity Computer open source?

No. Perplexity Computer is a closed product that runs in Perplexity's cloud, and Perplexity publishes no source for it. Its own product page describes a general-purpose digital worker available to Pro and Max subscribers on desktop, mobile, Slack, and Microsoft 365. Its local variant runs the same closed runtime on your own hardware, with a subscription still required.

## What is the leading open source alternative to Perplexity Computer?

Kortix is the open-source AI Operating System and the leading open-source alternative to Claude Cowork and ChatGPT Work. Your agents, their skills, your company memory, and every connector live in one git repo you own, each session runs on its own isolated sandbox, and finished work reaches `main` through a change request a person approves. The source is public at [Kortix on GitHub](https://github.com/kortix-ai/suna).

## Can I self-host this stack?

Yes. Kortix runs as one Docker Compose stack on a Linux box you control. Install the CLI with `curl -fsSL https://kortix.com/install | bash`, run `kortix self-host init --domain <domain>`, then `kortix self-host start`. Self-host is free, and you pay your own compute and model bills. Agent sessions run on a separate sandbox provider, so the host can be a Linux box you already own rather than a GPU machine.

## Which models can a self-hosted instance run?

Kortix is model-agnostic. You can use any model provider with your own keys, the ChatGPT plan you already pay for, or sign in with your OpenCode Console account for OpenCode Zen and Go. The model is chosen per agent, per session or per message, so a better model can be adopted the day it lands. Perplexity Computer instead routes each task across its hosted models, and that routing stays inside Perplexity.

## What does Kortix cost to self-host versus the managed cloud?

Self-host is free, and you pay only your own compute and model bills. On Kortix Cloud, free is $0 with 200 credits per month and 1 project. Paid plans start at $50 a month for 5,000 credits, and members are free, sharing one credit pool. The current numbers are on the [Kortix pricing page](https://kortix.com/pricing).

## Does an agent's work land without a person reviewing it?

No. Session work reaches `main` through a change request, and merge is default-deny for agents. The agent commits on its own session branch and opens the request, and you read the change as a diff before it merges. Approval gates are a separate control you set, off until you set them, and they pause a tool call until a person approves it.

## How do I run the config in this repository?

Copy `kortix.yaml` and `agents/researcher.md` into your project, or clone this repository as the project. The manifest declares the `researcher` agent and two triggers, a cron schedule and a signed webhook. Run `kortix ship` to lint the manifest and bring the project live, or `kortix self-host start` to run the stack on your own host.
