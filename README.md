# Skewed Cache & Pipelined CPU in Verilog

> 計算機結構（楊佳玲教授，臺大，2025 秋季）兩次 Verilog 個人作業的設計說明。
> Lab 2：五級管線 CPU，含前饋（forwarding）、load-use 停頓與分支清除（flush）。
> Lab 3：2 路偏斜相聯快取（skewed-associative cache），公開與隱藏測資全數通過，總週期數全班第 12。
> 依課程規定不公開原始碼。

Design notes for two individual Verilog labs from Computer Architecture (Prof. Chia-Lin Yang), National Taiwan University, Fall 2025.

| Lab | Topic | Result |
|---|---|---|
| [Lab 2](lab2-pipeline/) | Five-stage pipelined CPU | All 6 public tests match the reference output |
| [Lab 3](lab3-cache/) | 2-way skewed-associative data cache | All tests pass; 2,160 total cycles; 12th in class |

## Notes

- Source code is not published per course policy; available to reviewers upon request.
- The problem sets and testbench were provided by NTU Computer Architecture 2025 Fall.
- I used LLMs to assist with debugging (including reading waveforms), tidying up code, looking up design references, and turning instruction encodings into control-signal tables. The architecture and the implementation are my own.
