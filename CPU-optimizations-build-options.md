### Introduction

There are many processors architectures: x86 / x86-64 family, ARMv7, aarch64, etc.
Each architecture may support different additional instruction sets (SSE/AVX for x86, NEON for ARMv7).

OpenCV goal is to provide effective processors support, including separate optimized code paths for newest instruction sets.

Some OpenCV functions contains multiple code paths specialized for different processors features / instruction sets.
Selection of executed code path is based on auto-detection of available processor features.

### CMake options

These options are available since OpenCV &lt;next release&gt;.

Build options allow to specify **minimal** and **dispatched** optimization features sets:

* **Minimal** is required set of processor features. Executable will not run if some of these options are not available on target processor.

* **Dispatched** optimizations are additional code paths compiled into executable. They will be executed on supported processors only.

OpenCV uses these CMake variables to control supported optimization features:

* `CPU_BASELINE` - **minimal** set of required optimizations (if they are supported by C++ compiler)
  ```
  CPU_BASELINE=SSE2
  CPU_BASELINE=AVX
  ```
* `CPU_DISPATCH` - **dispatched** set of additional optimizations (if they are supported by C++ compiler)
  ```
  CPU_DISPATCH=SSE4_2,AVX
  CPU_DISPATCH=AVX
  CPU_DISPATCH=AVX,AVX2
  ```

**Note**: Flags `ENABLE_AVX`/`ENABLE_AVX2`/`ENABLE_POPCNT`/etc should not be used anymore. Use options above instead.

#### Advanced CMake options:

* `CPU_BASELINE_REQUIRE` - list of required baseline (minimal set) optimizations. Build fails if compiler doesn't support some of these optimizations.
* `CPU_DISPATCH_REQUIRE` - list of additional (dispatched set) optimizations. Build fails if compiler doesn't support some of these optimizations.
* `CPU_BASELINE_DISABLE` - list of completely disabled optimizations
* `CV_DISABLE_OPTIMIZATION` - disable all explicit optimized code (useful for debugging purposes)

#### CMake status of used optimizations:

OpenCV configuration status contains lines like these:
```
--   CPU/HW features:
--     Baseline:                    SSE SSE2 SSE3 SSSE3
--       requested:                 SSSE3
--     Dispatched code generation:  SSE4_1 AVX AVX2
--       requested:                 SSE4_1 AVX AVX2
```

### Source files layout

In general, C++ compilers don't support code generation of multiple enabled instruction sets for single source file.

Current layout of source files is:

* main source file: "cvfunction.cpp" - contains code dispatcher (see below) and general implementation
* shared header file: "cvfunction.hpp" - contains shared declarations used by generic and optimized code
* several files with optimized code (suffix `.<lowercase optimization name>.cpp`): "cvfunction.avx.cpp".

There is no requirement to implement all possible optimizations. Add function optimizations with better effort only.

#### Code dispatcher

Unwrapped version:

```
CV_CPU_CALL_AVX2(my_cv_function_avx2(...args...));
CV_CPU_CALL_FP16(my_cv_function_fp16(...args...));
CV_CPU_CALL_AVX(my_cv_function_avx(...args...));
CV_CPU_CALL_SSE4_2(my_cv_function_sse4_2(...args...));
CV_CPU_CALL_POPCNT(my_cv_function_popcnt(...args...));
CV_CPU_CALL_NEON(my_cv_function_neon(...args...));

... regular C++ implementation ...
```

These macro declarations are depend on CMake options:

* empty statement (in case of non-used or disabled optimization)
* conditional code execution: `if(checkHardwareSupport(CV_AVX)) ...`
* unconditional code execution in case of baseline optimization

#### AVX optimization note

Mixing of AVX and SSE code may provide significant performance reduction due registers sharing. Work around for this is to use `_mm256_zeroupper()` intrinsic:

```
#if CV_AVX && !defined CV_CPU_BASELINE_COMPILE_AVX
    _mm256_zeroupper();
#endif
```

#### Caution about C++ templates

All non-inline templates used in optimized code must be wrapped into separate (or anonymous) namespaces to prevent conflicts (linker will use one template's implementation only).

Unfortunately, there is no any warning from linker about this.

### Runtime environment variables

* `OPENCV_CPU_DISABLE` - allows to mask some processor features, so dispatched code doesn't run
  ```
  OPENCV_CPU_DISABLE=AVX2,AVX,FP16
  ```
