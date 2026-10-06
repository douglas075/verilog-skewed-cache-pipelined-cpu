# Lab 3: 2-Way Skewed-Associative Cache

## Scope

- **CPU:** single-cycle RV32 CPU extended from Lab 1 (adds branch comparison, PC selection, stall on cache miss, `ecall` handling).
- **Provided by the course:** data memory with 10-cycle latency and 128-bit blocks, testbench.
- **My work:** the CPU and the cache.

## Cache design

| Parameter | Value |
|---|---|
| Organization | 2-way skewed-associative, 4 sets per way |
| Line size | 16 bytes (4 words) |
| Capacity | 128 bytes of data |
| Indexing | way 0: `index`; way 1: `index XOR tag[1:0]` |
| Write policy | write-back, write-allocate |
| Replacement | invalid line first, otherwise one LRU bit per set (approximate for way 1) |

Controller states: `IDLE` (serve hits) → `WB` (write back dirty victim) → `ALLOC` (refill), and after `ecall`, `DRAIN` (write back all dirty lines) → `DONE`.

## Results

| Metric | Result |
|---|---|
| Tests | All pass (public and hidden) |
| Cycles | I1 419, I2 471, I3 596, I4 674; total 2,160 |
| Class ranking | 12th by total cycles |
| Area (Yosys + NanGate45) | CPU 11,123.6 (limit 12,000); cache 16,431.4 (limit 20,000) |
| Latches | 0 |

## Size sweep (I4)

| Sets per way | Cycles | Cache area |
|---:|---:|---:|
| 2 | 681 | 8,374.7 |
| **4** | **674** | **16,431.4** |
| 8 | 682 | 31,500.3 |
| 16 | 698 | 61,267.2 |
| 32 | 730 | 115,278.8 |

4 sets is fastest and within the area limit. Above 4 sets, each doubling adds exactly one cycle per added line (+8, +16, +32), which matches the drain step's one-cycle-per-line scan. This is an inference; miss counts were not measured.

## Report

[report.pdf](report.pdf). One sentence was revised after submission to remove an unmeasured hit-rate claim.
