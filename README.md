# Maxim Anisimov | HPC & Low-Level Python Specialist

![Assembly](https://img.shields.io/badge/ASM-x86_64-red)
![C++](https://img.shields.io/badge/C%2B%2B-17-blue)
![C#](https://img.shields.io/badge/C%23-10-blue)
![NumPy](https://img.shields.io/badge/NumPy-1.26+-blue)
![Numba](https://img.shields.io/badge/Numba-0.59+-green)
![CUDA](https://img.shields.io/badge/CUDA-12.x-red)
![LLVM](https://img.shields.io/badge/LLVM-IR-purple)

> Python is a remote control for LLVM kernels. Zero overhead in hot paths.

## Low Level Technical Stack (Strictly Typed & Pre-allocated)
*   **Compute:** I use np.empty with a custom allocator to ensure 64-byte alignment for AVX-512 registers on Zen 4, avoiding unaligned load penalties. Numba (`@njit`, `@parallel`), NumPy (**Structured Arrays**, DType Packing), CUDA.
*   **Memory:** `ctypes`, `np.memmap`, Cache Line Alignment (64-byte padding).
*   **Vectorization:** SIMD (AVX-512/AVX2), Stride-1 Access, Branch Elimination.
*   **Profiling:** `cProfile`, `valgrind`, **LLVM IR Inspection**.

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
