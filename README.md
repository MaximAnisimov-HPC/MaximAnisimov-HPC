# Maxim Anisimov | Principal Performance Architect
### High-Frequency Data Pipelines & CPU-Cycle Optimization

![Assembly](https://img.shields.io/badge/ASM-x86_64-red)
![SIMD](https://img.shields.io/badge/SIMD-Branchless%20Logic-red)
![AVX512](https://img.shields.io/badge/AVX512-Full%20Width%20Utilization-red)
![CUDA](https://img.shields.io/badge/CUDA-12.x-red)
![LLVM](https://img.shields.io/badge/LLVM-IR-purple)
![C++](https://img.shields.io/badge/C%2B%2B-17-blue)
![C#](https://img.shields.io/badge/C%23-10-blue)
![NumPy](https://img.shields.io/badge/NumPy-1.26+-blue)
![Numba](https://img.shields.io/badge/Numba-0.59+-blue)



> **"Turning Python into a low-level tool: I use LLVM and strong typing to eliminate interpreter overhead, reaching C++ level latency and 100% hardware utilization."**

### Low-Level Optimization & ASM Refinement
* **Asm-Level Surgical Refinement:** Manual elimination of `.LBB` jump labels and branch-heavy logic. I replace `if/else` with bitwise masking and `CMOV` to achieve zero-stall execution.
* **Precision SIMD Orchestration:** Overriding compiler heuristics to force **AVX-512 (zmm)** and **AVX2 (ymm)** utilization. I verify `vmovaps/vaddpd` density via manual **LLVM IR** tuning to ensure 8–32 FLOPs per cycle and **100% hardware saturation**
* **Cache-Aware Determinism:** Architecting hot paths with pre-allocation and strict type locking to bypass the Python interpreter and hit raw **C++ hardware latency**.
* **Instruction Audit:** Continuous verification of **IPC (Instructions Per Cycle)** to guarantee that every clock cycle is spent on computation, not overhead.


### Hardware-Centric Memory Architecture
* **Deterministic Runtime:** 100% pre-allocation at $t=0$. I eliminate heap fragmentation and **GC jitter** by enforcing zero-dynamic-resizing policies.
* **L1/L2 Cache Engineering:** Strict `Stride-1` access patterns and manual **64-byte padding** to neutralize **False Sharing** and optimize cache-line utilization.
* **Layout Enforcement:** Explicit memory contiguity (C/Fortran order) verified via **LLVM IR metadata** for deterministic data movement.
* **Type-Locked Pipelines:** Zero JIT runtime dispatch through strict `dtype` signatures and explicit **Interpreter Bypass** (no Python objects in `@njit` scopes).
* **Branchless Micro-Ops:** Transforming logic into SIMD-friendly arithmetic masking to maximize **IPC** and prevent pipeline stalls.


### Performance Credentials
*   [Scientific Computing with Python](https://freecodecamp.org/certification/maximanisimov/python-v9) | freeCodeCamp
*   **Focus**: Eliminating Python Object Overhead in Data Pipelines.
*   **Profiling:** `cProfile`, `line_profiler`, `numba.cuda.profiler`, `valgrind/memcheck`.
*   **Benchmarking:** Micro-benchmarking with `time.perf_counter()`, latency measurement, and memory profiling (`tracemalloc`).
*   **LLVM IR Analysis**: Manual inspection of generated assembly to verify vectorization efficiency.
