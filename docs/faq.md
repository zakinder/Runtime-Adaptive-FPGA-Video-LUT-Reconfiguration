# FAQ — Runtime-Adaptive FPGA Video LUT Reconfiguration

## Purpose

This FAQ answers common questions about the Runtime-Adaptive FPGA Video LUT Reconfiguration project and clarifies the current documentation-stage status of the repository.

## Questions

### What problem does this project solve?

The project addresses the difficulty of changing FPGA video LUT behavior while a live RGB video stream is running. It separates LUT preparation from activation so that updates can be staged, applied, and verified more safely.

### Why use a shadow LUT buffer?

A shadow LUT buffer allows new LUT data to be written without immediately affecting the active video-processing path. This reduces the risk of partial updates, visual glitches, and unstable output.

### What is the active LUT bank?

The active LUT bank is the memory or register bank currently driving the RGB mapping logic. It remains stable while the shadow buffer receives new data.

### What is command-indexed profile selection?

Command-indexed profile selection means that software can select a LUT profile or palette mode by writing a command value instead of rewriting the entire processing configuration each time.

### Why is diagnostic readback needed?

Diagnostic readback lets software verify the active command index, active LUT bank, update status, error status, and selected configuration state after an update.

### Is RTL included now?

Not yet. The repository is currently focused on documentation, architecture planning, publication preparation, and validation planning. RTL skeletons may be added in a future version.

### Is this a finished product?

No. This is a technical documentation and publication-preparation repository. Implementation, simulation, hardware validation, and diagrams are planned future stages.

### Can this be archived on Zenodo?

Yes. The repository structure is being prepared so a GitHub release can later be archived on Zenodo for DOI citation.

### Should patent review happen before more public disclosure?

Yes, if intellectual-property protection is important. Patent-sensitive implementation details should be reviewed with a qualified professional before wider disclosure.

## Status

Initial FAQ for project clarity and documentation support.
