# Maxim Anisimov | HPC & Low-Level Python Specialist

> "Python is just a remote control for LLVM kernels."

## Technical Stack (Strictly Typed & Pre-allocated)
*   **Compute:** Numba (@njit, @parallel), NumPy (Structured Arrays, memmap), CUDA (PyCUDA).
*   **Memory:** Explicit Memory Management (`ctypes`, `np.memmap`), Structured Arrays, Cache Line Alignment.
*   **Optimization:** SIMD Vectorization (AVX-512/SSE), L1/L2 Cache Locality, Stride-1 Access, Branch Prediction Avoidance.
*   **Architecture:** C/Fortran memory layout (`order='C'`/`F`), Manual Memory Management, LLVM IR Inspection.

### Performance Credentials
* 🎓 [Scientific Computing with Python (freeCodeCamp)]([https://freecodecamp.org](https://freecodecamp.org/certification/maximanisimov/python-v9))
*   🔥 **Focus**: Eliminating Python Object Overhead in Data Pipelines.
*   ⚡ **Profiling:** `cProfile`, `line_profiler`, `numba.cuda.profiler`, `valgrind/memcheck`.
*   📊 **Benchmarking:** Micro-benchmarking with `time.perf_counter()`, latency measurement, and memory profiling (`tracemalloc`).

## System Principles:
1.  **NO** dynamic lists or dicts in hot loops.
2.  **NO** `append()` calls. Buffers are pre-allocated at `t=0`.
3.  **ONLY** Numba-compiled functions for critical paths.
4.  **STRICT TYPE INFERENCE:** No `Any` types inside JIT scopes; explicit `dtype` declarations to prevent runtime type checks.
5.  **NO BRANCH MISPREDICTIONS:** Use arithmetic masking or conditional moves instead of `if/else` inside critical loops.
6.  **CONTIGUOUS MEMORY ACCESS:** All data passed to kernels must be C-contiguous (`order='C'`) unless explicit strides are calculated manually.
