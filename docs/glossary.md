# Glossary — Runtime-Adaptive FPGA Video LUT Reconfiguration

## Purpose

This glossary defines common technical terms used throughout the Runtime-Adaptive FPGA Video LUT Reconfiguration project. The goal is to keep terminology consistent across the README, architecture documents, register map, validation plan, and paper drafts.

## Terms

| Term | Definition |
|---|---|
| Active LUT Bank | The LUT memory or register bank currently used by the live RGB video-processing path. |
| Activation Control | Logic that safely applies a pending LUT update to the active processing state. |
| AXI4-Lite | A lightweight memory-mapped control interface commonly used for FPGA register access. |
| Command Index | A host-written value that selects a LUT profile, palette behavior, or runtime mode. |
| Diagnostic Readback | A software-visible mechanism for verifying active command, active bank, status flags, and applied LUT values. |
| Frame-Safe Activation | An update approach that applies configuration changes at a safe video timing boundary, such as frame or line boundary. |
| Host Software | Software running on a processor or external controller that writes configuration registers and reads status. |
| LUT | Lookup table used to transform, map, or select pixel/color values. |
| LUT Profile | A grouped set of LUT values or configuration parameters representing one color behavior or palette mode. |
| Profile ID | A software-visible identifier for a selected or loaded LUT profile. |
| Register Map | The set of memory-mapped control and status registers exposed to software. |
| RGB Mapping Logic | Hardware logic that applies active LUT behavior to incoming RGB pixel data. |
| Shadow LUT Buffer | A staging buffer that receives new LUT values before they are activated. |
| Shadow Valid | A status flag indicating that the shadow buffer contains a valid pending update. |
| Update Done | A status flag indicating that activation completed successfully. |
| Update Error | A status flag indicating that an activation request or command was invalid or failed. |

## Naming Guidance

Use these names consistently in documentation and future RTL:

```text
shadow_lut_buffer
active_lut_bank
command_index
activation_control
diagnostic_readback
rgb_mapping_logic
profile_id
update_done
update_error
```

## Status

Initial glossary for documentation consistency and future implementation traceability.
