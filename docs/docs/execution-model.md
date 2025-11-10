# SUDARSHAN Execution Model (v0.1)

SUDARSHAN uses a **deterministic circular dataflow** model.

## Core Concept
Computation moves around the ring of MMUs in a **clockwise** direction, while 
control and scheduling signals move **counter-clockwise** through SCUs.

This ensures:
- Predictable latency per operation
- No global synchronization barriers
- High sustained utilization

## Execution Cycle

1. The SCU issues a micro-op packet into the ring.
2. Data aligned with the op flows into the next MMU in the cycle.
3. Each MMU performs one step of computation (e.g., matmul tile or attention block).
4. The output is passed to the next MMU.
5. The process continues until the operation completes.

Because timing is **positional**, not **clock-synchronous**, a token of compute 
"rides the ring" rather than being scheduled dynamically.

## Result
This eliminates:
- Warp scheduling
- Hazard stalls
- High scheduling power overhead

And enables:
- ~90–98% utilization under transformer workloads.
