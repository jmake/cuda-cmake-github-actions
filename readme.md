# CUDA + Cmake example using Github Actions

This repo is a very simple CUDA application, used to GitHub Actions as a CI service for CUDA compilation.

This will **potentially** be expanded to investigate self-hosted runner(s) for running tests locally.

[![Ubuntu](https://github.com/ptheywood/cuda-cmake-github-actions/workflows/Ubuntu/badge.svg)](https://github.com/ptheywood/cuda-cmake-github-actions/actions?query=workflow%3AUbuntu)
[![Windows](https://github.com/ptheywood/cuda-cmake-github-actions/workflows/Windows/badge.svg)](https://github.com/ptheywood/cuda-cmake-github-actions/actions?query=workflow%3AWindows)

## Sample application

To be representative of a real world example this should include:

+ `cmake` for cross platform build tooling
+ `nvcc` to compile .cu code.
+ some form of test script?

## Compilation

```bash
mkdir -p build
cd build
cmake .. 
make
```

## Execution

```bash
cd build
./main
```

## Version Compatibility

CUDA is only supported with appropriate host compilers.

This support matrix can be found in the CUDA documentation, however, there are some obvious caveats related to the current state of github actions (at the time of writing)

+ [Windows-2019](https://github.com/actions/virtual-environments/blob/master/images/win/Windows2019-Readme.md#visual-studio-2019-enterprise)
    + Visual Studio `16.5.5` which maps to [`_MSC_VER 1925`](https://docs.microsoft.com/en-us/cpp/preprocessor/predefined-macros?view=vs-2019)
        + `CUDA >= 10.1`
            + `CUDA 10.0` requires `_MSC_VER` between `1700` and `1920`
+ [Ubuntu 18.04](https://github.com/actions/virtual-environments/blob/master/images/linux/Ubuntu1804-README.md#ubuntu-18044-lts)
    + GNU C++ `7.5.0`, `8.4.0` & `9.3.0` are available
    + CUDA `10.0+` are available in the apt repository.
        + You can use the older `1604` apt repo to enable `CUDA 8.0+`
+ [Ubuntu 20.04](https://github.com/actions/virtual-environments/blob/master/images/linux/Ubuntu2004-README.md#ubuntu-20044-lts)
    + GNU C++  `9.4.0`, `10.3.0` are available#
        + GNU C++ `10.3.0` leads to errors when using `<chrono>` with NVCC in `--std=C++17` mode. This has been addressed in GCC, but the patch hasn't made it to Ubuntu packaged GCC.
    + CUDA `11.0+` are available in the apt repository.
        + You can use the older `1804` apt repo to enable `CUDA 10.0+`, but this is an unsupported configuration which may lead to errors.
