# Micro-Op Scheduling in SUDARSHAN (v0.1)

In SUDARSHAN, SCUs are responsible for sequencing computation across MMUs
in a **deterministic cyclic pattern**. This avoids dynamic warp scheduling
complexity and ensures predictable execution latency.

## Key Idea

- Compute moves **clockwise** through the ring.
- Control and scheduling directives move **counter-clockwise**.
- SCUs assign **time-slots** (positions in the ring) rather than clock-driven dispatch.

## Scheduling Model

Each SCU maintains:
- A micro-op queue
- Data availability state
- Next-slot prediction from Scout cores

At every cycle:
1. SCU issues micro-op to the next MMU in the ring.
2. MMU executes the fused matmul/attention kernel.
3. Result moves to the next ring position.

No global synchronization is required.

## Benefits

- **High sustained utilization**
- **Low scheduling overhead**
- **No crossbar or mesh arbitration**
- **Scales linearly with chiplet count**
