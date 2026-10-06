# Lab 2: Five-Stage Pipelined CPU

## Scope

- **ISA:** the RV32 subset from Lab 1, plus `lw`, `sw`, `beq`, `bne`.
- **Provided by the course:** register file, PC register, instruction and data memory, testbench.
- **My work:** the CPU top level and all other modules (13 source files): four pipeline registers, control, ALU control, ALU, immediate generator, multiplexers, adder, forwarding unit, hazard detection unit.

## Design

**Forwarding.** Each ALU operand comes from a 4-input mux. The forwarding unit selects EX/MEM when the previous instruction writes the same non-zero register, otherwise MEM/WB under the same condition, otherwise the register file.

**Load-use stall.** If the instruction in EX is a load whose destination matches `rs1` or `rs2` in ID, the PC and IF/ID hold for one cycle and the control signals entering ID/EX are zeroed (a bubble).

**Branches.** `beq` and `bne` are resolved in ID. Fetch continues with PC + 4 (predict not taken); on a taken branch the PC is redirected and the instruction in IF/ID is replaced by a NOP. Branch operands are not forwarded into ID; the course test programs insert NOPs where needed.

## Verification

- 6 public test programs: the per-cycle register and memory dump is identical to the reference output.
- Yosys synthesis (NanGate45): 0 latches.
