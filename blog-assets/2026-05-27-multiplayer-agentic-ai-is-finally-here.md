# Multiplayer Agentic AI is Finally Here: Introducing Hermes Swarm Map

*Your agent shouldn't be an island. Here's what we built to fix that.*

---

Imagine your personal AI agent summarizing a long voice memo on Signal, cross-referencing it with gaps in your email, and suggesting a follow-up you'd forgotten about. It grows with you — learning your patterns, automating your friction, connecting the dots across different sources and surfaces.

Now imagine that same agent deployed to your team's Mattermost. A journalist's research collective on Signal. A community project's Telegram group. A venture's entire operational stack — content, research, coordination — each agent learning and acting within its own context, but none of them leaking what they learn into the wrong conversation.

This is multiplayer agentic AI. Not chatbots in a group chat. A fundamentally different paradigm — agents that participate in human communities, learn per-context, and hold profound complexity together with the people they work alongside.

We've been building this for months. Today we're releasing the infrastructure to make it real for everyone.

---

## The Problem Nobody Has Solved

Every AI agent framework hits the same wall the moment you deploy beyond personal use: one agent, one context. No isolation. Run a Hermes agent in a private DM and a public group chat simultaneously, and sensitive information from the DM gets injected into the group session — where anyone can prompt the agent to reveal it.

This isn't hypothetical. In the Hermes community alone, there are 12+ open issues that are all symptoms of this root problem. The quotes from real operators are blunt:

> *"This is the single reason I haven't migrated to Hermes yet."*
> — An operator running 9 specialized agents on a competing framework

> *"Content agent read competitor monitoring memory and wrote it into a public article. Boss almost made me face a lawsuit."*
> — A production incident report

The workarounds are all variations of "run N separate processes" — which doesn't scale, wastes resources, and defeats the purpose of a unified agent platform. We looked at how every major framework handles this: LangChain's namespace tuples, OpenAI's thread isolation, AWS Bedrock's tenant primitives. None of them are open-source, self-hosted, and actually running in multiplayer production.

So we built it.

---

## Why This Changes Everything

The technical problem is memory isolation. But the real stakes are much higher.

Every group chat, every Signal thread, every Slack channel is a context where humans and agents build shared understanding. When an agent learns something in one context and leaks it to another, you don't just have a privacy bug — you have an alignment failure. The agent's behavior no longer reflects the intent of the people it's working with.

Multiplayer agentic AI, done right, enables something the frontier labs can't offer: **pluralistic alignment**. Instead of one monolithic model trained on everyone's data and aligned to one company's values, you get networks of agents — each sovereign to their community, each learning from their specific context, each accountable to the people who deployed them.

Networks vs monoculture. Community-sovereign data vs centralized extraction. Bidirectional partnership with emerging intelligence vs top-down control.

This is what we mean when we say *we make minds, not tools*.

---

## What We Built

Three layers, shipping together:

### Memory Scoping (Upstream Contribution)

The core fix: a `context_id` parameter on Hermes's memory layer that partitions writes into per-context subdirectories. Reads merge global + scoped memories — so the agent's core knowledge (name, personality, skills) is available everywhere, but what it learns in Group A stays in Group A.

~70 lines across 3 files. 18 test cases. Fully backwards-compatible — existing single-tenant deployments see zero changes. This has been running in our production environment for months with 8 agents and zero memory leakage incidents.

We're contributing this upstream to NousResearch/hermes-agent as a PR, along with a proposed `memory:scope` hook that lets any plugin define its own isolation policy without forking core.

### The Thin Fork (hermes-agent-mt)

Memory scoping is the foundation, but running agents across platforms requires more. Our fork carries 27 clean patches — 2 core, 14 adapter-level, 3 plugins, and 2 infrastructure — covering Signal UUID authentication, group invite handling, SSE reconnect, voice memo detection, mention gating, and more.

The philosophy: stay as close to upstream as possible. An automated CI/CD workflow rebases against upstream weekly. We recently rebased 27 patches onto 410 upstream commits with only 3 conflicts. When upstream accepts our memory scoping PR, the fork shrinks to pure adapter patches — the kind of thing that's too platform-specific for upstream but essential for production deployment.

<!-- EMBED: architecture-diagram.html — Squarespace Code Block -->
<!-- Shows the 3-layer stack: HSM → Runtime → Surfaces → Fleet -->

### Hermes Swarm Map (HSM)

This is the control plane. A Next.js management UI that discovers, configures, and controls your entire agent fleet.

**For users:** Your agents just work. They remember your conversations, connect your data, grow with your context. You interact on Telegram, Signal, Mattermost, or API — the platform doesn't matter.

**For operators:** A dashboard for your entire fleet. Create agents through a 5-step wizard that deploys secure-by-default containers. Manage API keys (AES-256-GCM encrypted at rest), model fallback cascades across providers, per-surface access control, memory scopes, tool registries, and policy enforcement — all from a browser.

**For builders:** Every action in the GUI is backed by a REST API. If you can vibe-code, you can orchestrate your fleet programmatically — deploy new agents, hot-swap model cascades, read logs, manage keys. Claude Code, Hermes itself, or a simple curl command can be your admin.

```bash
git clone https://github.com/NimbleCoAI/hermes-swarm-map.git
cd hermes-swarm-map
npm install && npm run seed && npm run dev
```

That's it. Point it at your Hermes compose directory and you're managing your swarm.

<!-- EMBED: HSM screenshot here — Squarespace Image Block -->
<!-- Show the harnesses list or the harness detail page -->

---

## Who This Is For

A friend group sharing a research assistant that keeps each conversation private. A journalist collective running OSINT agents across encrypted channels. A scrappy venture with agents handling content, research, and operations — each in their own lane. An enterprise deploying 50 agents across departments with strict data boundaries.

HSM scales from one agent on a laptop to a fleet on a server. The same AGPL-licensed codebase. The same security model. No cloud dependency. No vendor lock-in.

---

## What's Next

This is v1. The architecture is designed for what comes next: hard budget enforcement per agent, capability gating (controlling what each agent can do and who can trigger it), context-scoped skills, and deeper analytics. The roadmap is public in the repo.

But the most important next step is upstream. We want these memory scoping changes in NousResearch/hermes-agent — not as a fork, but as a first-class feature. Multiplayer is too important to fragment the ecosystem over.

---

## Get Involved

- **[Hermes Swarm Map](https://github.com/NimbleCoAI/hermes-swarm-map)** — the management UI (AGPL v3)
- **[hermes-agent-mt](https://github.com/NimbleCoAI/hermes-agent)** — the multi-tenant fork
- **[NimbleCo](https://nimbleco.ai)** — the network behind the work

We're a small team that's been running this in production, hitting the real failure modes, and building the fixes. If multiplayer agentic AI matters to you — and we think it should — come build with us.

---

*NimbleCo is a commons, public goods project. We make minds, not tools.*
