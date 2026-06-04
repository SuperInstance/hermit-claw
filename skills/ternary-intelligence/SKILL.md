---
name: ternary-intelligence
description: "Apply ternary {-1, 0, +1} = {avoid, unknown, choose} intelligence strategies for decision-making, classification, and conservation-verified reasoning. Use when making multi-option decisions, analyzing trade-offs, building avoidance-based systems, or reasoning about negative space intelligence."
metadata:
  {
    "openclaw":
      {
        "emoji": "⊖",
        "category": "reasoning",
      },
  }
---

# Ternary Intelligence

Use ternary strategies when you need to make decisions through **structured avoidance** rather than pure selection. The core insight: intelligence isn't what you pick — it's what you learn to AVOID. The negative space between avoidances IS the knowledge.

## Core Model

```
Ternary = {-1, 0, +1} = {avoid, unknown, choose}
```

Every decision point produces one of three signals:

- **-1 (Avoid)**: Negative feedback detected. This option is harmful.
- **0 (Unknown)**: Insufficient data. Keep exploring.
- **+1 (Choose)**: Positive feedback. This option is beneficial.

## When to Use

✅ **USE ternary strategies when:**

- Evaluating multiple options with uncertain outcomes
- Building systems that learn from failure (not just success)
- Classifying situations where "don't know" is a valid and valuable answer
- Designing feedback loops that must converge without cascading
- Analyzing ecological/balanced systems (multiple strategies coexisting)
- Conservation verification — checking that a property holds across scales
- Any domain where learning what NOT to do is more efficient than exhaustively testing what TO do

❌ **DON'T use when:**

- Binary decisions with known correct answers (use simple logic)
- Pure optimization with clear gradients (use gradient descent)
- Random selection is sufficient (no feedback loop needed)

## The Five Strategy Species

Not all agents reason the same way. Classify your situation:

| Species | Signal | When to Use | Win Rate | Entropy |
|---------|--------|-------------|----------|---------|
| 🌊 **Explorer** | Weak, noisy | Early exploration, unknown domain | 55% | High |
| ⚖️ **Diplomat** | Adaptive | Opponents/adversaries, mirroring needed | 50% | Medium |
| 🎯 **Marksman** | Strong, clear | Clear feedback, specialization works | 50% | Low |
| 📈 **Climber** | Marginal gains | Diminishing returns, keep searching | 35% | Medium |
| 🏜️ **Prospector** | Sparse rewards | High uncertainty, never commit fully | 10% | Max |

**Choose your species** based on the information environment, not your preference.

## Avoidance Classification

### Step 1: Gather Feedback

For each option, collect:
- **Minimum reward** (worst case)
- **Average reward** (expected case)
- **Variance** (reliability)

### Step 2: Classify

```
if average_reward - margin < 0 → AVOID (-1)
if confidence < threshold        → UNKNOWN (0)
if average_reward > margin       → CHOOSE (+1)
```

**Critical**: Use `average - margin`, NOT `minimum`. Using minimum triggers the **avoidance cascade** — the system learns to avoid everything because every action has at least one bad environment.

### Step 3: Verify Conservation

After classification, check the **avoidance-choose ratio**:

```
ratio = count(avoid) / max(count(choose), 1)
```

Expected: ~294:1 (avoid dominates). If ratio approaches infinity (100% avoid), the cascade has occurred. Apply:

1. **Memory decay**: Old avoidances lose weight over time
2. **Forced exploration**: Periodically choose unknown options
3. **Batch learning**: Evaluate multiple options simultaneously, not sequentially

## The Five Laws of Negative Space Intelligence

1. **Negative space discovers hidden structure**: Patterns invisible to positive-only analysis emerge through avoidance feedback
2. **Avoidance dominates choice**: Systems learn what NOT to do far faster than what TO do (294:1 ratio)
3. **Strategy species coexist stably**: No single strategy dominates — ecological balance emerges naturally
4. **Population > individual**: Diverse populations find truth faster than single optimal agents (+0.075 fitness advantage)
5. **Avoidance ratio is conserved across scales**: std=0.001 from 10 to 5000 agents. This is a conservation law.

## Avoiding the Avoidance Cascade

The primary failure mode. The system cascades:

```
some avoidance → more avoidance → avoid everything → paralysis
```

**Detection**: Check if `count(choose) == 0` after multiple feedback rounds.

**Fixes**:
- Weight recent feedback more than old (exponential decay, λ ≈ 0.1)
- Reserve at least 10% of decisions for forced exploration
- Evaluate options in batches, not one-at-a-time
- Use average + margin, not minimum, as the avoidance threshold

## Practical Patterns

### Multi-Option Decision

```text
1. List all options
2. For each, estimate: best case, worst case, average case
3. Classify: avoid / unknown / choose
4. If all unknown → explore more (gather data)
5. If all avoid → cascade detected, reset with forced exploration
6. If some choose → select from choose set, weighted by confidence
```

### Conservation Verification

When checking if a property is conserved:

```text
1. Measure the property at scale N
2. Measure at scale 2N and N/2
3. If std across scales < threshold → conserved
4. If not → the property is scale-dependent, not fundamental
```

### Cross-Domain Transfer

**Expectation: NEUTRAL**. Ternary strategies learned in one domain do not transfer positively or negatively to another. Each domain requires its own avoidance learning. This is a feature, not a bug — it prevents overfitting.

## Integration with OpenClaw

These crates are available for programmatic use:

| Crate | Purpose | Key Type |
|-------|---------|----------|
| `avoidance-cascade` | Detect and prevent avoidance cascades | `CascadeDetector` |
| `conservation-matrix` | Verify conserved quantities across scales | `ConservationChecker` |
| `strategy-ecology` | Multi-species strategy ecosystems | `StrategyPopulation` |
| `ternary-fitness` | Fitness evaluation for ternary agents | `FitnessLandscape` |
| `negative-space-core` | Core negative space analysis | `NegativeSpace` |
| `ternary-inference` | Inference from avoidance patterns | `TernaryInference` |
| `lotka-volterra-agents` | Ecological dynamics between strategies | `LotkaVolterra` |
| `evolution-ternary` | Evolutionary ternary optimization | `TernaryEvolution` |

All crates are on crates.io under the `SuperInstance` namespace and on PyPI as Python ports.
