# Self-hosting or managed cloud for an open source agent stack

Kortix is open source, and you can run the same open-source AI Operating System either on hardware you control or on Kortix Cloud. This guide compares the two paths by what you run, what you own, and what it costs, so you can pick by the operations you are willing to carry.

## The two paths run the same software

Self-hosting moves the whole system onto a machine you control. Managed Kortix Cloud runs the same open-source code as a service. Agents, skills, memory, connector config, and triggers are files in one git repo either way, so the project is portable between the two. You can start on the managed cloud and move to your own VPC or on-prem network later without rewriting the system, because the repo, the agents, and the skills are the same files.

## Where to run a self-hosted instance

The same install runs on a laptop, a VPS, your VPC, or your own rack. Pick the host by what you can maintain.

| Host | Good for | You provide | You manage |
| --- | --- | --- | --- |
| Laptop | A first trial on your own files | Docker and the install | Backups |
| VPS | A shared instance for a team | A small Linux server | Uptime, upgrades, backups |
| VPC | Work inside your cloud account | Your cloud account | Network rules and keys |
| On-prem | Regulated environments | Your own hardware | Patching, capacity, recovery |
| Kortix Cloud | Starting with nothing to run | Nothing | Nothing |

Self-hosting keeps your data and credentials on your side. The repo, the memory files, and the brokered connector credentials all sit on machines you own, and you bring your own model keys. The trade is operational: you own uptime, upgrades, and isolation, which means patching the host, watching the Docker Compose stack, and backing up the data yourself. Because the agents reach models through an API, the host can be a Linux box you already own rather than a GPU machine.

## What each path costs

Self-host is free. You pay for the machine you run it on and the model APIs you attach, at rates you set. On Kortix Cloud, free is $0 with 200 credits per month and 1 project. Paid plans start at $50 a month for 5,000 credits, and members are free, sharing one credit pool. The current numbers are on the [Kortix pricing page](https://kortix.com/pricing).

Neither path makes compute or models free. The comparison is about software floors and meters: a self-hosted seat costs nothing in software and grows only with the work you run, while the managed cloud trades a monthly credit floor for zero operations of your own.

## What stays the same

Whichever host you pick, the security model is the same. One isolated sandbox per session, each with its own isolated machine and branch. Session work reaches `main` through a change request, and merge is default-deny for agents. Secrets are encrypted at rest with a key per project, and connector credentials are brokered server-side and never enter the machine. Approval gates are off until you set them, and you set each tool to allow, ask, or block.

The [self-hosting walkthrough](https://opensourceperplexitycomputer.com/self-hosting) on the campaign site expands on the install, and the [Kortix docs](https://kortix.com/docs/host) carry the reference.
