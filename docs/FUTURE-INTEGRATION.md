# Future Integration: hermit-claw

## Current State
ZeroClaw — a Rust-based personal AI assistant fork targeting $10 hardware with <5MB RAM. 100% Rust, 100% agnostic. Built by the Harvard/MIT/Sundai.Club community. The lightweight alternative to OpenClaw.

## Integration Opportunities

### With construct-core Layer 0
hermit-claw's minimal footprint (<5MB RAM, $10 hardware) is the perfect runtime for construct-core's BareMetalConstruct tier. An ESP32 or Raspberry Pi Zero running hermit-claw implements Layer 0: O(1) lookup queries, static capability introspection, zero allocation. hermit-claw IS the bare-metal agent.

### With room-as-codespace
When a room needs to run on edge hardware too constrained for full OpenClaw, hermit-claw takes over. The same construct-core traits, the same ternary-protocol messages, but compiled for minimal hardware. hermit-claw agents walk between rooms just like OpenClaw agents — they just carry less luggage.

### With claw (OpenClaw)
hermit-claw and OpenClaw are complementary runtimes: OpenClaw for Layer 2 rooms (Codespaces, full compute), hermit-claw for Layer 0 rooms (ESP32, Raspberry Pi). Both implement construct-core traits, so the agent's identity and skills are portable between them. The fleet uses both.

## Dormant Ideas Now Unlockable
hermit-claw was a standalone project. Now construct-core provides the trait interface that makes hermit-claw a first-class fleet member. ternary-protocol provides the communication layer. The Rust implementation is actually an advantage — construct-core's traits are Rust-native, so hermit-claw implements them directly with zero FFI overhead.

## Potential in Mature Systems
Every bare-metal device in the fleet runs hermit-claw. ESP32s, Raspberry Pis, Arduino-adjacent boards — all are fleet members via hermit-claw. They tick ternary cells, respond to ternary-protocol messages, and report to PLATO. The fleet extends to the physical world through hermit-claw.

## Cross-Pollination Ideas
- **pincherOS**: OS concepts for hermit-claw's bare-metal runtime
- **claw**: OpenClaw for heavy rooms, hermit-claw for light rooms
- **lever-runner-wasm**: WASM build patterns inform hermit-claw's minimal deployment

## Dependencies for Next Steps
- Implement construct-core's BareMetalConstruct trait
- Add ternary-protocol message handling
- Test on ESP32 and Raspberry Pi hardware
