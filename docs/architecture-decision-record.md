# Architecture Decision Record — Runtime-Adaptive FPGA Video LUT Reconfiguration

## Purpose

This document records key architecture decisions for the Runtime-Adaptive FPGA Video LUT Reconfiguration project. The goal is to preserve design reasoning as the project moves from documentation into RTL, validation, and publication stages.

## ADR-001 — Separate Control Path from Video Path

### Decision

Use a host-controlled configuration path separate from the live RGB video-processing path.

### Reason

The video path must remain deterministic while software writes new configuration data. Separation reduces the risk that partial configuration writes affect active pixel processing.

### Consequence

The design requires explicit synchronization between configuration updates and active video behavior.

## ADR-002 — Use Shadow LUT Buffering

### Decision

Stage pending LUT updates in a shadow LUT buffer before activation.

### Reason

Direct writes to the active LUT bank may expose incomplete or unstable values to the live stream.

### Consequence

The design requires shadow-valid tracking and activation control logic.

## ADR-003 — Use an Active LUT Bank

### Decision

Use an active LUT bank to drive the live RGB mapping logic.

### Reason

The active bank provides stable lookup behavior while the shadow buffer is being modified.

### Consequence

Bank switching or controlled copy logic is required.

## ADR-004 — Use Command-Indexed Profile Selection

### Decision

Use a command index to select runtime LUT profiles or palette behavior.

### Reason

A command index allows profile selection without requiring the full processing path to be rewritten for every mode change.

### Consequence

The design requires valid command decoding, invalid command handling, and active command readback.

## ADR-005 — Add Diagnostic Readback

### Decision

Provide diagnostic readback registers for active state verification.

### Reason

Runtime reconfiguration is safer when software can confirm which profile, bank, and status flags are active.

### Consequence

The design requires additional status and readback mux logic.

## ADR-006 — Treat Register Map as Representative Until RTL Exists

### Decision

Document the register map as representative during the planning stage.

### Reason

Exact register fields may change during RTL implementation and validation.

### Consequence

Future RTL updates must synchronize register names, field widths, and behavior with documentation.

## Status

Initial architecture decision record for documentation and future implementation traceability.
