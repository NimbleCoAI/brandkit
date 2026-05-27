# Launch Thread — Twitter/X

---

**1/**
Multiplayer agentic AI is finally here.

We've been running 8 AI agents across Telegram, Signal, and Mattermost for months — each learning in its own context, none of them leaking into each other.

Today we're open-sourcing the infrastructure.

🧵

---

**2/**
The problem: every AI agent framework treats multi-tenant as an afterthought.

Run one agent in a DM and a group chat? Memory leaks between them. 12+ open issues in Hermes alone. One operator's content agent leaked competitor intel into a public article.

We fixed this at the storage layer.

---

**3/**
What we built:

→ Memory scoping — per-context isolation, ~70 lines, 18 tests, backwards-compatible. Contributing upstream to @NousResearch.

→ Thin fork — 27 clean patches, automated weekly rebase. Stays current with upstream, carries zero unnecessary divergence.

→ Hermes Swarm Map — open-source management UI for your entire agent fleet.

---

**4/**
HSM in action:

• Create agents through a wizard → secure by default
• Model cascades across providers (Anthropic, OpenAI, Bedrock, Ollama)
• API keys encrypted at rest
• Per-surface access control (who can talk to which agent, in which group)
• Full REST API — if you can curl, you can manage your swarm

[screenshot]

---

**5/**
Who is this for?

A friend group sharing a research agent. A journalist collective on Signal. A venture running content + research + ops agents. An enterprise with 50 agents across departments.

Same codebase. Laptop to server. No cloud. No vendor lock-in. AGPL v3.

---

**6/**
The bigger picture: multiplayer AI + community-sovereign data = pluralistic alignment.

Not one model aligned to one company's values. Networks of agents — each sovereign to their community, each learning from their context, each accountable to the people who deployed them.

We make minds, not tools.

---

**7/**
Get started:

git clone https://github.com/NimbleCoAI/hermes-swarm-map.git
npm install && npm run seed && npm run dev

Fork: github.com/NimbleCoAI/hermes-agent
Blog: nimbleco.ai/blog

Come build with us.

---

# Hermes Discord Post

---

Hey folks — we've been running a multi-tenant Hermes deployment in production for months (8 agents across Telegram, Signal, and Mattermost) and today we're open-sourcing the full stack.

**What we're releasing:**

1. **Memory scoping** — a `context_id` parameter that partitions memory per-context. ~70 lines, 18 tests, fully backwards-compatible. We're preparing a PR for upstream.

2. **hermes-agent-mt** — our clean fork with 27 patches (2 core + 14 adapter + 3 plugins + 2 infra). Automated weekly rebase against upstream. Recently rebased onto 410 commits with 3 conflicts.

3. **Hermes Swarm Map** — open-source Next.js management UI for Hermes fleets. Create, configure, monitor, restart agents from a browser. Full REST API. Encrypted key management. Model cascades. Policy enforcement.

We've filed an issue describing the multi-tenant problem in detail, including how other frameworks handle it and our proposed `memory:scope` hook. We'd love to contribute this upstream rather than maintaining a permanent fork.

Links:
- HSM: https://github.com/NimbleCoAI/hermes-swarm-map
- Fork: https://github.com/NimbleCoAI/hermes-agent
- Blog: https://nimbleco.ai/blog
- NimbleCo: https://nimbleco.ai

Happy to answer questions. We've hit most of the failure modes described in the existing multi-tenant issues — 28279, 9514, 4726, 14162, 17068 — and have working fixes for all of them.
