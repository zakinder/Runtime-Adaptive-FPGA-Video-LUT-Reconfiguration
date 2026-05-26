# LUT Reconfiguration Flow — Runtime-Adaptive FPGA Video LUT Reconfiguration

## Purpose

This document describes the LUT reconfiguration flow used in the Runtime-Adaptive FPGA Video LUT Reconfiguration system. The flow defines how LUT profile data is prepared, written, buffered, activated, and verified while the live video stream continues operating.

## Reconfiguration Objective

The main objective is to allow color-mapping behavior to change at runtime without stopping or corrupting the active RGB video stream.

## High-Level Flow

```text
Host Software
    |
    v
Write LUT Profile Data
    |
    v
Store Values in Shadow LUT Buffer
    |
    v
Select Command Index
    |
    v
Trigger Safe Activation
    |
    v
Update Active LUT Bank
    |
    v
Process Live RGB Stream
    |
    v
Read Back Active Configuration

## Step 1 — Host Writes LUT Profile Data

The host software writes LUT profile values through the control interface. These values may represent compressed max, mid, and min color-boundary entries or other RGB transformation parameters.

## Step 2 — Shadow LUT Buffer Receives Updates

New LUT data is first stored in a shadow buffer instead of being applied directly to the active video path. This prevents partial or unstable LUT writes from affecting the live stream.

## Step 3 — Command Index Selects Profile

A command index is used to select the intended LUT profile or palette behavior. This allows multiple profiles to be addressed without rewriting the full processing path.

## Step 4 — Activation Control Applies Update

Once the shadow buffer contains a valid configuration, the activation control logic transfers or switches the selected LUT profile into the active LUT bank.

## Step 5 — Active LUT Bank Drives Video Mapping

The active LUT bank supplies the currently selected lookup behavior to the RGB mapping logic. Incoming pixels are processed according to the active LUT configuration.

## Step 6 — Diagnostic Readback Verifies State

The diagnostic readback path allows software to confirm the active LUT values, selected command index, and applied configuration state.

## Technical Benefit

This flow separates LUT preparation from LUT activation. As a result, the system can update color behavior safely while preserving live video continuity.

## Status

Initial LUT reconfiguration flow description for documentation and publication preparation.


After this file, add:

```text
docs/diagnostic-readback.md