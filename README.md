# hormozi-skills

**Turn any business idea into a complete, sellable offer — using Alex Hormozi's frameworks.**

![License](https://img.shields.io/badge/license-MIT-blue)
![Claude Code](https://img.shields.io/badge/Claude%20Code-compatible-blueviolet)
![Platform](https://img.shields.io/badge/platform-Claude%20Code%20%7C%20Codex%20%7C%20Cursor-lightgrey)
![Inspired by](https://img.shields.io/badge/inspired%20by-Alex%20Hormozi-orange)

---

> A skill library for coding agents. Plug it in, describe your business, and get a complete offer system — market research, offer structure, pricing, pitch, hooks and landing page — proposed for review, then written only with approval.

---

## The Problem

Building a compelling offer is hard. Most founders, coaches, and consultants either:

- Write vague offers that don't convert — *"I help people grow their business"*
- Price wrong — too low to be taken seriously, too high without justification
- Skip the sales layer entirely — no hooks, no pitch, no landing page copy

**hormozi-skills** solves this end-to-end. One orchestrator, five specialized subagents, 17 skills, 11 output files.

---

## Security-hardened fork

This fork retains the **17 marketing skills** and the orchestrator with five subagents. The unrelated `create-plugin` scaffolding skill was removed. The orchestrator no longer declares terminal access.

- **Default: project-only**. Use a dedicated, non-sensitive directory and install only the skills you need.
- **No global install** and no automatic shell or installation commands.
- **Claude Code**: the checked-in `.claude/settings.json` applies **when this repository is the project being opened**. If you install the skills as a plugin in another project, its security rules **do not follow the plugin**; configure that project's permissions separately.
- **Codex**: the checked-in `.codex/config.toml` uses a read-only sandbox and approvals when this repository is the active trusted project; it does **not** automatically configure Codex in other projects.
- **Output**: Markdown in `output/` only, after explicit approval. Never overwrite an existing output without permission.
- **No client secrets**: provide only synthetic or redacted marketing input. Never assume the model has verified external research.

See [SECURITY.md](SECURITY.md) for the threat model, exact enforced versus advisory boundaries and deployment checklist. See [UPSTREAM_PIN.md](UPSTREAM_PIN.md) for the reviewed source commit and manual update policy.

## Quick Start

### Claude Code: use this fork, not upstream

In Claude Code's plugin command interface (these are plugin commands, **not shell commands**):

```text
/plugin marketplace add ElijahGhost-dotcom/hormozi-skills
/plugin install hormozi-skills@hormozi-skills
```

**Important:** configure the *host project's* permissions first; the plugin installer does not copy this fork's project security settings into that host project. For the strongest default, open this fork itself as the isolated workspace and explicitly review any requested file writes.

### Codex

Use a dedicated project in **read-only** mode with approval required for file changes; the included project config is an example for operating from this repository. If using the plugin from another directory, configure that directory independently. Review proposed generated files before saving them.

### Manual project-scoped use

Copy only the needed `skills/<name>/` folders to the target project's `.claude/skills/` using your file manager. If needed, copy only the declared agent Markdown files to that project's `.claude/agents/`. Do not install globally. Copy the security settings **only after checking they do not override project requirements**, and check `/permissions` before use.

---

## 📦 What You Get

Up to 11 output files proposed for `output/` in one session (each write requires approval):

| File | What's Inside |
|------|--------------|
| `MARKET_RESEARCH.md` | Hypothesized niche, pain map, validation plan (verify externally) |
| `OFFER.md` | Full Grand Slam Offer — avatar, obstacles, solution map, value stack |
| `OFFER_ANGLES.md` | 8 positioning angles, ranked |
| `OFFER_AUDIT.md` | Score per dimension + priority fixes |
| `VALUE_PERCEPTION.md` | Improved naming, packaging, framing |
| `BONUS_STACK.md` | Objection-killing bonus structure with perceived value |
| `PRICING.md` | Value-anchored price, tiers, justification story |
| `OBJECTIONS.md` | Hidden beliefs, belief shifts, DM-ready responses |
| `PITCH.md` | Short / medium / long pitch versions |
| `HOOKS.md` | 30+ hooks across 10 types, ranked |
| `LANDING_PAGE.md` | Full landing page copy, section by section |

---

## 🧠 Skills Library

Use any skill standalone — no orchestrator needed:

| Skill | Purpose |
|-------|---------|
| `hormozi-offer` | Build a Grand Slam Offer from scratch → `OFFER.md` |
| `hormozi-pitch` | Pitch deck and sales narrative |
| `hormozi-hooks` | Hook and headline generation (30+ hooks) |
| `audit-offer` | Score and rewrite an existing weak offer |
| `bonus-stack` | Build a bonus stack that kills objections |
| `business-model` | Choose and structure the right business model |
| `dfy-dwy-diy` | Frame offer as DFY / DWY / DIY tiers |
| `effort-reduction` | Reduce perceived effort in the offer |
| `idea-to-product` | Turn rough idea into productized offer |
| `landing-page-copy` | Generate landing page copy from an existing offer |
| `market-research` | Research market pain and demand signals |
| `objection-destroyer` | Map and neutralize common objections |
| `offer-angles` | Generate multiple positioning angles |
| `pricing-strategy` | Price anchoring and packaging |
| `productize` | Productize a service business |
| `value-accelerator` | Increase perceived value |
| `value-perception` | Improve how value is communicated |

> [!TIP]
> Skip the orchestrator and call any skill directly: `/audit-offer`, `/pricing-strategy`, `/landing-page-copy` — each works standalone with no prior context needed.

---

## 🔀 Agent System

```
hormozi-orchestrator
├── sub-market    → MARKET_RESEARCH.md
├── sub-offer     → OFFER.md + OFFER_ANGLES.md
├── sub-value     → OFFER_AUDIT.md + VALUE_PERCEPTION.md + BONUS_STACK.md
├── sub-pricing   → PRICING.md + OBJECTIONS.md
└── sub-sales     → PITCH.md + HOOKS.md + LANDING_PAGE.md
```

**Dependency order:** market → offer → (value ∥ pricing) → sales

The orchestrator detects your funnel stage (idea / broken offer / needs sales layer / service scaling) and runs only the subagents you need.

---

## ⚙️ How It Works

1. **Intake** — give the orchestrator anything: a raw idea, existing offer, brain dump, or sales page
2. **Interview** — focused questions one at a time, each with a suggested answer
3. **Stage detection** — classifies your situation (Stage A–E), shows which subagents will run
4. **Delegation** — spawns subagents in dependency order, passing structured briefs
5. **Summary** — produces `output/SUMMARY.md`: one-paragraph offer, key decisions, top 3 actions, best hook to use today

---

## Repo Structure

```
hormozi-skills/
├── skills/     # 17 standalone agent skills
├── agents/     # Orchestrator + 5 subagents
├── output/     # Generated offer documents (starts empty)
└── input/      # Drop existing offers, notes, or sales pages here
```

---

## Who This Is For

- Founders, coaches, consultants, and freelancers building offers
- Anyone applying Hormozi's methodology who wants AI execution, not just AI advice
- Coding agents running offer-generation pipelines

## Who This Is Not For

- Generic copywriters looking for fill-in-the-blank templates — this thinks, it doesn't just fill
- Developers needing a code library — this is prompt-based, agent-native
- People who want a one-shot answer without iteration — the orchestrator interviews you

---

## Frameworks

Built on Alex Hormozi's offer methodology from *$100M Offers* and *$100M Leads*:

- Grand Slam Offer construction
- Dream outcome × likelihood × time delay × effort equation
- Obstacle → solution reversal
- Value stack and bonus engineering
- Guarantee design (unconditional / conditional / effort-based)
- Price anchoring and perceived value
- Hook architecture (pattern interrupt, identity, outcome, curiosity)

---

## Credits

Inspired by Alex Hormozi's work. Built for coding agents by [@alexsmedile](https://github.com/alexsmedile).
