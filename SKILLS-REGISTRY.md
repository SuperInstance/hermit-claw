# SKILLS-REGISTRY.md — Ternary Ecosystem Skills

All skills in hermit-claw that extend the agent's capabilities with ternary intelligence.

## Registered Skills

| Skill | Category | Emoji | Description | Powered By |
|-------|----------|-------|-------------|------------|
| [ternary-intelligence](skills/ternary-intelligence/SKILL.md) | Reasoning | ⊖ | Apply ternary {-1, 0, +1} strategies for decision-making, classification, and conservation-verified reasoning | `ternary-inference`, `conservation-matrix`, `negative-space-core`, `strategy-ecology`, `ternary-fitness` |
| [ternary-builder](skills/ternary-builder/SKILL.md) | Development | 🔧 | Build new ternary ecosystem crates with templates, conventions, and testing requirements | All ternary crates (scaffolding) |

## Powering Crates

These Rust crates (published on crates.io under `SuperInstance`) provide the runtime libraries that back each skill:

| Crate | Version | Purpose | Key Type / Trait |
|-------|---------|---------|-------------------|
| `avoidance-cascade` | `0.1.x` | Detect and prevent avoidance cascades | `CascadeDetector` |
| `conservation-matrix` | `0.1.x` | Verify conserved quantities across scales | `ConservationChecker` |
| `strategy-ecology` | `0.1.x` | Multi-species strategy ecosystems | `StrategyPopulation` |
| `ternary-fitness` | `0.1.x` | Fitness evaluation for ternary agents | `FitnessLandscape` |
| `negative-space-core` | `0.1.x` | Core negative space analysis | `NegativeSpace` |
| `ternary-inference` | `0.1.x` | Inference from avoidance patterns | `TernaryInference` |
| `lotka-volterra-agents` | `0.1.x` | Ecological dynamics between strategies | `LotkaVolterra` |
| `evolution-ternary` | `0.1.x` | Evolutionary ternary optimization | `TernaryEvolution` |

Python equivalents are available on PyPI.

## Skill ↔ Crate Mapping

```
ternary-intelligence ──► ternary-inference (core reasoning)
                    ──► conservation-matrix (verification)
                    ──► negative-space-core (analysis)
                    ──► strategy-ecology (multi-agent)
                    ──► ternary-fitness (evaluation)
                    ──► avoidance-cascade (safety)

ternary-builder ──► All crates (templates, conventions, tests)
```

## Adding a New Skill

1. Create `skills/<skill-name>/SKILL.md` with YAML frontmatter (`name`, `description`, `metadata`)
2. Follow the pattern from existing skills — include: when to use, inputs, outputs, examples
3. Reference the powering crates with version numbers in a table
4. Add the skill to the registry table above
5. Add the skill ↔ crate mapping if new crates are involved
6. Test by symlinking into `~/.openclaw/skills/` and verifying the agent picks it up

See [CONTRIBUTING.md](CONTRIBUTING.md) for full contribution guidelines.

## Installation

```bash
# Symlink skills into OpenClaw (recommended)
ln -s "$(pwd)/skills/ternary-intelligence" ~/.openclaw/skills/
ln -s "$(pwd)/skills/ternary-builder" ~/.openclaw/skills/

# Or copy
cp -r skills/ternary-intelligence ~/.openclaw/skills/
cp -r skills/ternary-builder ~/.openclaw/skills/
```

## Verification

After installation, confirm skills are registered:

```bash
# OpenClaw
openclaw skills list

# ZeroClaw
zeroclaw skills list
```

Both skills should appear with their descriptions.
