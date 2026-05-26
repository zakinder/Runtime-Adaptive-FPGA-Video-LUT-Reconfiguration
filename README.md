# Runtime-Adaptive FPGA Video LUT Reconfiguration

Runtime-adaptive FPGA video LUT reconfiguration system for real-time RGB stream processing, compressed color-boundary storage, shadow LUT buffering, command-indexed palette profiles, and diagnostic readback.

## Overview

This project presents a runtime-adaptive FPGA-based video lookup table reconfiguration architecture for real-time RGB video stream processing. The system supports dynamic LUT updates while maintaining live video operation.

## Key Features

- Real-time RGB video stream processing
- Runtime LUT reconfiguration
- Compressed max/mid/min color-boundary storage
- Dynamic RGB order mapping per pixel
- Command-indexed palette profile switching
- Shadow LUT buffering for safe activation
- Diagnostic readback verification
- AXI4-Lite controlled register interface

## Technical Purpose

The purpose of this project is to demonstrate a hardware-controlled method for dynamically changing video color transformation behavior without stopping the live video stream.

## System Architecture

The architecture includes:

1. Host control interface
2. AXI4-Lite register control
3. LUT command index decoder
4. Shadow LUT buffer
5. Active LUT bank
6. RGB pixel mapping logic
7. Diagnostic readback path

## Applications

- FPGA-based video processing
- Embedded vision systems
- Real-time color correction
- Camera pipeline enhancement
- Hardware-accelerated image processing
- Adaptive display systems

## Repository Structure

```text
docs/
src/
rtl/
testbench/
images/
README.md
LICENSE