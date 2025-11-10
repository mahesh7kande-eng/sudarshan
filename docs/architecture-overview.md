# SUDARSHAN — Circular Chiplet GPU Architecture

SUDARSHAN is an **open hardware AI compute architecture** designed around a 
**deterministic circular dataflow** instead of traditional GPU warp schedulers 
or mesh interconnects.

The goal is simple:

> **High AI performance with predictable latency, simple wiring, and modular chiplets.**

Modern GPUs are powerful but extremely complex:
- Large crossbar or mesh interconnects
- Dynamic warp schedulers
- High power cost per mm²
- Difficult to scale down or modularize

SUDARSHAN takes a different approach.

## Core Principles

- **SCUs (Simple Control Units)** coordinate compute
- **MMUs (Matrix Multiply Units)** perform fused matmul + attention workloads
- **Scout Cores** prefetch + predict execution flow
- All units communicate on a **circular ring interconnect**
- Execution is **position-based, not time-based**
- The system achieves **high sustained utilization** with **low scheduling overhead**

This makes SUDARSHAN well-suited for:
- LLM inference
- On-device AI
- Edge compute
- Energy-efficient reasoning accelerators
- Open silicon research

## Why Circular?

Typical GPU interconnects (mesh / crossbar) grow wiring complexity **quadratically**.
SUDARSHAN uses a **ring**, where wiring complexity grows **linearly**.

This makes:
- Layout simpler
- Power lower
- Timing closure easier
- Chiplet scaling straightforward

## High-Level Architecture

doc
