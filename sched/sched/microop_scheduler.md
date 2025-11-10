# Micro-Op Scheduling in SUDARSHAN (v0.1)

The SCU (Simple Control Unit) does not "dispatch" instructions dynamically.
Instead, it issues **micro-ops into fixed time slots** in the circular ring.

## Scheduling Rules

- The ring has 32 MMU positions.
- Each SCU controls 4 MMUs (total of 8 SCUs).
- Each SCU owns specific **time-slot windows** for issuing micro-ops.

### Example Slot Assignment (Ring Size = 32)

| SCU | Controls MMUs | Slot Window |
|----|--------------|------------|
| SCU0 | MMU0–3  | Slots 0–3   |
| SCU1 | MMU4–7  | Slots 4–7   |
| SCU2 | MMU8–11 | Slots 8–11  |
| SCU3 | MMU12–15| Slots 12–15 |
| SCU4 | MMU16–19| Slots 16–19 |
| SCU5 | MMU20–23| Slots 20–23 |
| SCU6 | MMU24–27| Slots 24–27 |
| SCU7 | MMU28–31| Slots 28–31 |

## Key Insight
Because each SCU controls a **fixed region of the ring**, no arbitration is required.

This enables:
- Zero-conflict deterministic scheduling
- No central scheduler
- No global interconnect pressure
