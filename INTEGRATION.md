# INTEGRATION.md — Ternary Ecosystem × OpenClaw (hermit-claw)

This document explains how ternary intelligence crates plug into OpenClaw's skill system and how the hermit-claw fork serves as the bridge.

## Architecture

```
┌─────────────────────────────────────────┐
│           OpenClaw Agent Runtime         │
│                                         │
│  ┌─────────────────┐  ┌──────────────┐ │
│  │ ternary-         │  │ ternary-     │ │
│  │ intelligence     │  │ builder      │ │
│  │ (reasoning skill)│  │ (dev skill)  │ │
│  └────────┬────────┘  └──────┬───────┘ │
│           │                  │         │
│           ▼                  ▼         │
│  ┌────────────────────────────────────┐ │
│  │     Ternary Crates (crates.io)     │ │
│  │  avoidance-cascade                 │ │
│  │  conservation-matrix               │ │
│  │  strategy-ecology                  │ │
│  │  ternary-fitness                   │ │
│  │  negative-space-core               │ │
│  │  ternary-inference                 │ │
│  │  lotka-volterra-agents             │ │
│  │  evolution-ternary                 │ │
│  └────────────────────────────────────┘ │
└─────────────────────────────────────────┘
```

## What's in This Repo

### Skills Directory (`skills/`)

Two OpenClaw-compatible skills:

| Skill | Purpose | When It Activates |
|-------|---------|-------------------|
| `ternary-intelligence` | Teaches the agent how to reason using ternary strategies, avoidance classification, and conservation verification | Decision-making, trade-off analysis, classification tasks, avoidance reasoning |
| `ternary-builder` | Provides templates and patterns for creating new ternary ecosystem crates | Building new Rust/Python/C crates in the ternary ecosystem |

### How Skills Plug In

OpenClaw skills are self-contained `SKILL.md` files with YAML frontmatter:

```yaml
---
name: skill-name
description: "When to activate this skill"
metadata: { "openclaw": { "emoji": "⊖" } }
---
```

The agent runtime:
1. Scans skill descriptions at session start
2. When a user request matches a skill's description, loads the full SKILL.md
3. Follows the instructions in the skill's body

**To install these skills in OpenClaw:**

Copy or symlink the skill directories into the OpenClaw skills directory:

```bash
# Option 1: Symlink (recommended, stays in sync)
ln -s /path/to/hermit-claw/skills/ternary-intelligence ~/.openclaw/skills/
ln -s /path/to/hermit-claw/skills/ternary-builder ~/.openclaw/skills/

# Option 2: Copy
cp -r skills/ternary-intelligence ~/.openclaw/skills/
cp -r skills/ternary-builder ~/.openclaw/skills/
```

Or install globally:

```bash
# System-wide OpenClaw skills
ln -s /path/to/hermit-claw/skills/ternary-intelligence /usr/local/lib/openclaw/skills/
ln -s /path/to/hermit-claw/skills/ternary-builder /usr/local/lib/openclaw/skills/
```

## The Ternary Model

### Core Insight

```
Ternary = {-1, 0, +1} = {avoid, unknown, choose}
```

Intelligence isn't what you pick — it's what you learn to AVOID. The negative space between avoidances IS the knowledge.

### Why It Matters for Agents

1. **Efficiency**: Learning to avoid bad options is 294x faster than finding the best option
2. **Conservation**: Key metrics (avoidance ratio) are conserved across scales — what works at 10 agents works at 5000
3. **Ecological balance**: No single strategy dominates — the system naturally maintains diversity
4. **Cascade resistance**: With proper safeguards (memory decay, forced exploration), the system won't paralyze itself

### The Five Laws

1. Negative space discovers hidden structure
2. Avoidance dominates choice (294:1)
3. Strategy species coexist stably
4. Population > individual
5. Avoidance ratio is conserved across scales

## Available Crates

All crates are published on crates.io and can be added as dependencies:

```toml
[dependencies]
avoidance-cascade = "0.1"
conservation-matrix = "0.1"
strategy-ecology = "0.1"
ternary-fitness = "0.1"
negative-space-core = "0.1"
ternary-inference = "0.1"
lotka-volterra-agents = "0.1"
evolution-ternary = "0.1"
```

Python equivalents available on PyPI.

## Extending the Ecosystem

To add a new ternary crate:

1. Use the `ternary-builder` skill for templates and conventions
2. Follow the naming conventions (see skill)
3. Ensure ≥15 tests with conservation, cascade, and property invariants
4. Publish to crates.io under `SuperInstance`
5. Push to `https://github.com/SuperInstance/<crate-name>`
6. Update the crate table in both skills

## Hermit-Claw's Role

Hermit-claw is the OpenClaw fork (ZeroClaw) that bridges the ternary ecosystem with the agent runtime. It:

- Hosts the skill definitions that teach agents about ternary reasoning
- Serves as the integration point between ternary crates and the agent's decision-making
- Can be extended to use ternary crates natively in the agent loop (future work)

### Future Integration Points

- **Agent loop**: Use `ternary-inference` for action selection in the main agent loop
- **Memory**: Use `avoidance-cascade` detection in memory retrieval (avoid recalled-bad strategies)
- **Tool selection**: Use ternary classification for tool choice (avoid tools that failed in similar contexts)
- **Conservation monitoring**: Use `conservation-matrix` to verify agent behavior stays within bounds
