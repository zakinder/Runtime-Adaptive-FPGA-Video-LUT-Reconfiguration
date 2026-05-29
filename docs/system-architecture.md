# System Architecture — Runtime-Adaptive FPGA Video LUT Reconfiguration

## Purpose

This document describes the system architecture for the Runtime-Adaptive FPGA Video LUT Reconfiguration project. The architecture is designed to support runtime color-profile updates in an FPGA-based real-time RGB video processing pipeline.

## High-Level Architecture

The system consists of a host-controlled configuration path and a live video-processing path. The configuration path updates LUT values, command indices, and control registers. The video path continues processing RGB pixel data while LUT changes are prepared and activated safely.

## Major Components

### 1. Host Control Interface

The host interface provides software-level control for loading LUT profiles, selecting command indices, triggering updates, and requesting diagnostic readback.

### 2. AXI4-Lite Register Interface

The AXI4-Lite interface exposes control and status registers to the host system. These registers may be used to configure LUT entries, command selections, activation controls, and verification reads.

### 3. Command Index Decoder

The command index decoder selects a predefined or loaded palette profile based on a command value. This allows multiple LUT behavior profiles to be selected without rewriting the entire configuration each time.

### 4. Shadow LUT Buffer

The shadow LUT buffer stores new or updated LUT values before they are activated. This helps prevent unstable or partial LUT updates from affecting the live video stream.

### 5. Active LUT Bank

The active LUT bank provides the currently applied lookup values used by the live RGB pixel-processing path.

### 6. RGB Mapping Logic

The RGB mapping logic applies the selected LUT behavior to incoming RGB pixel data. The mapping may dynamically arrange max, mid, and min color-boundary values into RGB order per pixel.

### 7. Diagnostic Readback Path

The diagnostic readback path allows software to verify active LUT values, selected command profiles, and applied configuration states.

## Data Flow

```text
Host Software
    |
    v
AXI4-Lite Register Interface
    |
    v
Command Index Decoder
    |
    v
Shadow LUT Buffer
    |
    v
Activation Control
    |
    v
Active LUT Bank
    |
    v
RGB Mapping Logic
    |
    v
Live Video Output
```

## Control Flow

1. Host software writes LUT profile data.
2. LUT data is stored in the shadow LUT buffer.
3. Host selects a command index or profile.
4. Activation control validates and applies the update.
5. Active LUT bank switches to the updated values.
6. RGB mapping logic processes the live video stream.
7. Diagnostic readback confirms active configuration.

## Design Benefit

The architecture separates LUT preparation from LUT activation. This allows the FPGA video pipeline to continue operating while new LUT behavior is loaded, checked, and activated safely.

## Status

Initial architecture description for documentation and publication preparation.
