# Diagram Plan — Runtime-Adaptive FPGA Video LUT Reconfiguration

## Purpose

This document defines the planned diagram set for the Runtime-Adaptive FPGA Video LUT Reconfiguration project. These diagrams will support README presentation, technical publication, white paper figures, and future release documentation.

## Diagram Standards

Recommended format:

- 16:9 aspect ratio for presentation reuse
- PNG for GitHub display
- SVG for editable/vector publication use when available
- Clear engineering block-diagram layout
- Separate control path and video path where possible
- Consistent labels matching the documentation

## Planned Diagrams

| File | Purpose |
|---|---|
| `images/system-block-diagram.png` | Shows the full control path and live video path. |
| `images/lut-reconfiguration-flow.png` | Shows the sequence from host write to diagnostic readback. |
| `images/shadow-buffer-activation.png` | Shows how pending LUT data is staged before activation. |
| `images/active-shadow-bank-switching.png` | Shows active/shadow bank separation and switching. |
| `images/register-map-overview.png` | Shows the main control and status register groups. |
| `images/diagnostic-readback-path.png` | Shows how active state is read back by software. |
| `images/live-video-pipeline-integration.png` | Shows the LUT layer inside a live RGB video pipeline. |
| `images/validation-flow.png` | Shows the planned simulation and validation path. |

## Priority Order

1. `system-block-diagram.png`
2. `lut-reconfiguration-flow.png`
3. `active-shadow-bank-switching.png`
4. `diagnostic-readback-path.png`
5. `validation-flow.png`

## Suggested Visual Labels

Use these labels consistently across diagrams:

- Host Software
- AXI4-Lite Register Interface
- Command Index Decoder
- Shadow LUT Buffer
- Activation Control
- Active LUT Bank
- RGB Mapping Logic
- Live Video Output
- Diagnostic Readback

## Status

Initial diagram planning document for future visual architecture assets.
