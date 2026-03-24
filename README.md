# Maxim Anisimov | Principal Performance Architect
### High-Frequency Data Pipelines & CPU-Cycle Optimization

![Assembly](https://img.shields.io/badge/ASM-x86_64-red)
![LLVM](https://img.shields.io/badge/LLVM-IR-purple)
![SIMD](https://img.shields.io/badge/SIMD-Branchless%20Logic-red)
![AVX512](https://img.shields.io/badge/AVX512-Full%20Width%20Utilization-green)
![CUDA](https://img.shields.io/badge/CUDA-12.x-red)
![C++](https://img.shields.io/badge/C%2B%2B-17-blue)
![C#](https://img.shields.io/badge/C%23-10-blue)
![NumPy](https://img.shields.io/badge/NumPy-1.26+-blue)
![Numba](https://img.shields.io/badge/Numba-0.59+-green)



> **"Turning Python into a low-level tool: I use LLVM and strong typing to eliminate interpreter overhead, reaching C++ level latency and 100% hardware utilization."**

### Low-Level Optimization & ASM Refinement
* **Asm-Level Surgical Refinement:** Manual elimination of `.LBB` jump labels and branch-heavy logic. I replace `if/else` with bitwise masking and `CMOV` to achieve zero-stall execution.
* **Extreme SIMD Vectorization:** Overriding compiler heuristics to force **AVX-512 (zmm)** and **AVX2 (ymm)** utilization. I hand-tune **LLVM IR** to ensure high-density **Vector Ops** and 100% compute throughput.
* **Cache-Aware Determinism:** Architecting hot paths with pre-allocation and strict type locking to bypass the Python interpreter and hit raw **C++ hardware latency**.
* **Instruction Audit:** Continuous verification of **IPC (Instructions Per Cycle)** to guarantee that every clock cycle is spent on computation, not overhead.


## Performance Optimisation: Zero-Overhead Architecture

### Memory Optimisation
*   **Pre-allocation at $t=0$**: Zero use of `list.append()` or dynamic resizing to prevent heap fragmentation.
*   **Contiguity**: Strict `order='C'` or `order='F'` enforcement for Stride-1 sequential access.
*   **Memory Barriers**: Manual management of object boundaries; **Optimization verified via LLVM IR inspection** to ensure L1/L2 cache locality.

### Kernel Optimization
*   **Type Locking**: Explicit `dtype` signatures to eliminate JIT runtime dispatch.
*   **Branchless Logic**: Arithmetic masking and conditional moves instead of `if/else` for SIMD-friendly pipelines.
*   **Interpreter Bypass**: Python acts only as a controller; no Python objects enter the `@njit` scope.

### Performance Credentials
*   [Scientific Computing with Python](https://freecodecamp.org/certification/maximanisimov/python-v9) | freeCodeCamp
*   **Focus**: Eliminating Python Object Overhead in Data Pipelines.
*   **Profiling:** `cProfile`, `line_profiler`, `numba.cuda.profiler`, `valgrind/memcheck`.
*   **Benchmarking:** Micro-benchmarking with `time.perf_counter()`, latency measurement, and memory profiling (`tracemalloc`).
*   **LLVM IR Analysis**: Manual inspection of generated assembly to verify vectorization efficiency.
