---
name: ternary-builder
description: "Build new ternary intelligence crates — Rust libraries implementing avoidance learning, conservation verification, strategy ecology, and negative space reasoning. Use when creating new crates in the ternary ecosystem or extending existing ones."
metadata:
  {
    "openclaw":
      {
        "emoji": "🔧",
        "category": "development",
      },
  }
---

# Ternary Builder

Create new crates for the ternary intelligence ecosystem. The ecosystem uses ternary {-1, 0, +1} = {avoid, unknown, choose} as its fundamental unit.

## When to Use

✅ **USE this skill when:**

- Building a new Rust crate in the ternary ecosystem
- Porting a ternary crate to Python or C
- Extending an existing ternary crate with new features
- Creating tests for ternary logic

## Crate Structure

Every ternary crate follows this layout:

```text
crate-name/
├── Cargo.toml
├── README.md
├── src/
│   └── lib.rs        # or main.rs for binaries
└── tests/
    └── integration.rs
```

## Cargo.toml Template

```toml
[package]
name = "crate-name"
version = "0.1.0"
edition = "2021"
license = "MIT OR Apache-2.0"
description = "One-line description of what this crate does"
repository = "https://github.com/SuperInstance/crate-name"
keywords = ["ternary", "avoidance", "negative-space"]
categories = ["algorithms", "science"]

[dependencies]
# Keep dependencies minimal. Prefer stdlib.

[dev-dependencies]
# Test-only deps go here
```

## Core Types

### Ternary Value

```rust
/// The fundamental unit of ternary intelligence.
#[derive(Debug, Clone, Copy, PartialEq, Eq, Hash)]
pub enum Ternary {
    Avoid = -1,    // Negative feedback → don't do this
    Unknown = 0,   // Insufficient data → explore more
    Choose = 1,    // Positive feedback → do this
}
```

### Agent

```rust
/// A ternary agent that makes decisions and learns from feedback.
pub struct Agent {
    /// Strategy encoded as ternary vector
    strategy: Vec<Ternary>,
    /// Fitness score
    fitness: f64,
    /// Memory of past avoidances (with decay)
    avoidance_memory: Vec<f64>,
}
```

### Fitness Landscape

```rust
/// Evaluates how well a strategy performs in an environment.
pub trait FitnessLandscape {
    fn evaluate(&self, strategy: &[Ternary]) -> f64;
    fn environment_id(&self) -> &str;
}
```

## Testing Requirements

Every crate must have **≥15 tests** covering:

1. **Unit tests** — each public function/method
2. **Edge cases** — empty inputs, single elements, maximum sizes
3. **Conservation tests** — verify conserved quantities hold
4. **Cascade tests** — verify avoidance cascades are detected/prevented
5. **Property tests** — invariants that should always hold

### Test Template

```rust
#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_basic_classification() {
        // Positive → Choose
        assert_eq!(Ternary::classify(1.0, 0.5, 0.1), Ternary::Choose);
        // Negative → Avoid
        assert_eq!(Ternary::classify(-1.0, 0.5, 0.1), Ternary::Avoid);
        // Uncertain → Unknown
        assert_eq!(Ternary::classify(0.0, 0.5, 0.1), Ternary::Unknown);
    }

    #[test]
    fn test_conservation_invariant() {
        // The avoidance ratio should be approximately conserved
        // across different population sizes
        let r10 = avoidance_ratio(population(10));
        let r100 = avoidance_ratio(population(100));
        let r1000 = avoidance_ratio(population(1000));
        let std = standard_deviation(&[r10, r100, r1000]);
        assert!(std < 0.05, "Conservation violated: std = {std}");
    }

    #[test]
    fn test_no_cascade() {
        // System should never reach 100% avoidance
        let mut system = TernarySystem::new();
        for _ in 0..100 {
            system.learn(&feedback());
        }
        assert!(system.choose_count() > 0, "Avoidance cascade detected!");
    }
}
```

## Naming Conventions

| Pattern | Example | Use For |
|---------|---------|---------|
| `ternary-*` | `ternary-fitness` | Core ternary operations |
| `*-cascade` | `avoidance-cascade` | Cascade detection/prevention |
| `*-matrix` | `conservation-matrix` | Matrix/structured data |
| `*-ecology` | `strategy-ecology` | Multi-agent ecosystems |
| `*-core` | `negative-space-core` | Fundamental abstractions |
| `*-inference` | `ternary-inference` | Reasoning/inference |
| `*-transfer` | `strategy-transfer` | Cross-domain analysis |

## Publishing Checklist

1. `cargo test` — all tests pass
2. `cargo clippy -- -D warnings` — no warnings
3. `cargo fmt --check` — formatted
4. README.md exists with: description, usage example, API summary
5. `cargo publish --dry-run` — no errors
6. `cargo publish` — publish to crates.io
7. Push to `https://github.com/SuperInstance/<crate-name>`

## Python Port Pattern

```python
# crate_name/__init__.py
"""Python port of Rust crate-name."""

from .core import Ternary, Agent, classify

__all__ = ["Ternary", "Agent", "classify"]
__version__ = "0.1.0"
```

Use `maturin` for Rust-backed ports, pure Python for algorithmic ports.

## C Port Pattern

```c
// include/crate_name.h
#ifndef CRATE_NAME_H
#define CRATE_NAME_H

typedef enum {
    TERNARY_AVOID = -1,
    TERNARY_UNKNOWN = 0,
    TERNARY_CHOOSE = 1
} ternary_value_t;

#endif
```

## Key Invariants to Maintain

1. **Avoidance ratio ≈ 294:1** — systems should learn avoidance faster than choice
2. **Conservation across scales** — key metrics stable from 10 to 5000 agents
3. **Species coexistence** — all strategy types should survive in mixed populations
4. **No cascade** — systems should never reach 100% avoidance under normal operation
5. **Neutral transfer** — cross-domain strategy transfer should be ~0 (neither positive nor negative)
