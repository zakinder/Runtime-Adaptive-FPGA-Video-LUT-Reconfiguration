# Register Map — Runtime-Adaptive FPGA Video LUT Reconfiguration

## Purpose

This document defines a representative register map for the Runtime-Adaptive FPGA Video LUT Reconfiguration system. The register map is intended for an AXI4-Lite style memory-mapped control interface.

## Register Map Summary

| Offset | Register Name | Access | Purpose |
|---:|---|---|---|
| `0x00` | `CONTROL` | RW | Global control bits for enable, reset, and activation trigger |
| `0x04` | `STATUS` | RO | Runtime status, update flags, and error indicators |
| `0x08` | `COMMAND_INDEX` | RW | Selects LUT profile, palette command, or runtime mode |
| `0x0C` | `PROFILE_ID` | RW | Identifies the selected LUT/profile group |
| `0x10` | `LUT_WRITE_ADDR` | RW | Address/index for writing shadow LUT entries |
| `0x14` | `LUT_WRITE_DATA` | RW | Data value written into the shadow LUT buffer |
| `0x18` | `LUT_WRITE_CTRL` | RW | Write strobe and shadow-valid control |
| `0x1C` | `ACTIVE_BANK` | RO | Identifies the LUT bank currently driving the video path |
| `0x20` | `READBACK_SELECT` | RW | Selects diagnostic readback source |
| `0x24` | `READBACK_DATA` | RO | Returns selected diagnostic or LUT state data |
| `0x28` | `ERROR_STATUS` | RO/W1C | Reports invalid command, activation, or update errors |
| `0x2C` | `VERSION` | RO | Design version or build identifier |

## `CONTROL` Register — `0x00`

| Bit | Field | Access | Description |
|---:|---|---|---|
| 0 | `enable` | RW | Enables runtime LUT processing path |
| 1 | `soft_reset` | RW | Requests local control-block reset |
| 2 | `activate_update` | RW | Triggers activation of pending shadow LUT data |
| 3 | `clear_status` | RW | Clears selected status flags |
| 31:4 | `reserved` | RO | Reserved for future use |

## `STATUS` Register — `0x04`

| Bit | Field | Access | Description |
|---:|---|---|---|
| 0 | `enabled` | RO | Runtime processing path enabled |
| 1 | `shadow_valid` | RO | Shadow LUT contains valid pending update data |
| 2 | `update_busy` | RO | Activation sequence is in progress |
| 3 | `update_done` | RO | Last activation completed successfully |
| 4 | `update_error` | RO | Last update encountered an error |
| 5 | `frame_sync_done` | RO | Frame-safe activation event completed |
| 31:6 | `reserved` | RO | Reserved for future use |

## `COMMAND_INDEX` Register — `0x08`

| Bits | Field | Access | Description |
|---:|---|---|---|
| 7:0 | `command_index` | RW | Selects the active LUT command or palette profile |
| 31:8 | `reserved` | RO | Reserved for future use |

## `PROFILE_ID` Register — `0x0C`

| Bits | Field | Access | Description |
|---:|---|---|---|
| 15:0 | `profile_id` | RW | User-defined profile identifier |
| 31:16 | `reserved` | RO | Reserved for future use |

## LUT Write Sequence

1. Write target LUT entry index to `LUT_WRITE_ADDR`.
2. Write LUT data to `LUT_WRITE_DATA`.
3. Pulse write control through `LUT_WRITE_CTRL`.
4. Repeat until the shadow profile is complete.
5. Set command/profile selection.
6. Trigger activation through `CONTROL.activate_update`.
7. Verify state through `STATUS` and diagnostic readback.

## Diagnostic Readback Sources

| Select Value | Readback Source |
|---:|---|
| `0x00` | Active command index |
| `0x01` | Active bank ID |
| `0x02` | Shadow valid state |
| `0x03` | Update status flags |
| `0x04` | Active profile ID |
| `0x05` | Selected LUT entry value |
| `0x06` | Error status |
| `0x07` | Version/build ID |

## Notes

This register map is representative and may be refined during RTL implementation. Exact address widths, field widths, and behavior should be synchronized with the RTL and validation plan.
