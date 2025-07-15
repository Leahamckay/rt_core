# RT Core

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)

RT Core is a modern raytracing framework built on top of [OxC3 (Oxsomi Core 3)](https://github.com/Oxsomi/core3), providing high-level abstractions for developing real-time raytracing applications.

## Features

- **Cross-Platform Support**: Windows, Linux, macOS, Android, and iOS
- **Multiple Graphics APIs**: Vulkan, DirectX 12, and Metal
- **Raytracing Capabilities**:
  - Hardware-accelerated raytracing pipelines
  - Inline raytracing support
  - Bottom-Level Acceleration Structures (BLAS)
  - Top-Level Acceleration Structures (TLAS)
- **Modern Rendering Pipeline**:
  - Compute and graphics pipelines
  - Multi-sample anti-aliasing (MSAA)
  - Bindless resource management
  - Shader compilation and resource binding
- **Performance Optimizations**:
  - SIMD instruction support (SSE, AVX, NEON)
  - GPU command buffer management
  - Efficient memory management
- **Development Tools**:
  - Real-time debugging and profiling
  - Shader hot-reloading
  - Comprehensive test suite

## Quick Start

### Prerequisites

- CMake 3.13.0+
- Conan 2.0+
- C++20 compatible compiler
- Vulkan/DirectX 12 capable graphics drivers

### Building

#### Windows
```cmd
git clone --recursive https://github.com/Leahamckay/rt_core.git
cd rt_core
build.bat Debug True False False False
```

#### Linux/macOS
```bash
git clone --recursive https://github.com/Leahamckay/rt_core.git
cd rt_core
./build.sh Debug True False False False
```

#### Android
```bash
python build_android.py
```

### Running the Demo

After building, run the test application:

- **Windows**: `build/Debug/windows/x64/bin/rt_core.exe`
- **Linux**: `build/Debug/linux/x64/bin/rt_core`

The demo showcases various raytracing features including:
- Real-time ray-traced reflections
- Hardware-accelerated raytracing
- Atmospheric rendering
- Multi-threaded command buffer recording

## Architecture

RT Core is structured as a high-level wrapper around OxC3, providing:

- **Graphics Abstraction Layer**: Unified interface across graphics APIs
- **Resource Management**: Automatic reference counting and lifecycle management
- **Raytracing Primitives**: BLAS/TLAS creation and management
- **Pipeline Management**: Compute, graphics, and raytracing pipeline abstractions
- **Memory Management**: Efficient GPU memory allocation and streaming

## Documentation

- [Contributing Guide](CONTRIBUTING.md) - How to contribute to the project
- [Build Instructions](CONTRIBUTING.md#building-the-project) - Detailed build setup
- [API Examples](tst/test.c) - Sample usage and demonstrations

## Examples

### Creating a Simple Raytracing Pipeline

```c
// Create BLAS for geometry
BLASRef *blas;
GraphicsDeviceRef_createBLASExt(
    device,
    ERTASBuildFlags_DefaultBLAS,
    EBLASFlag_DisableAnyHit,
    ETextureFormatId_RG16f, 0,
    ETextureFormatId_R16u,
    sizeof(Vertex),
    vertexBuffer,
    indexBuffer,
    NULL,
    CharString_createRefCStrConst("Geometry BLAS"),
    &blas
);

// Create TLAS for scene
TLASRef *tlas;
GraphicsDeviceRef_createTLASExt(
    device,
    ERTASBuildFlags_DefaultTLAS,
    NULL,
    instanceList,
    false,
    NULL,
    CharString_createRefCStrConst("Scene TLAS"),
    &tlas
);

// Create raytracing pipeline
PipelineRef *rtPipeline;
GraphicsDeviceRef_createPipelineRaytracingExt(
    device,
    &stages,
    binaries,
    &hitGroups,
    raytracingInfo,
    CharString_createRefCStrConst("RT Pipeline"),
    EPipelineFlags_None,
    NULL,
    &rtPipeline,
    NULL
);
```

## Platform Support

| Platform | Graphics API | Status |
|----------|--------------|--------|
| Windows  | DirectX 12   | ✅ Full |
| Windows  | Vulkan       | ✅ Full |
| Linux    | Vulkan       | ✅ Full |
| macOS    | Metal        | ✅ Full |
| macOS    | Vulkan       | ✅ Via MoltenVK |
| Android  | Vulkan       | ✅ Full |
| iOS      | Metal        | ✅ Full |

## License

RT Core is dual-licensed:

- **[GPL-3.0](LICENSE)** for open source projects
- **Commercial License** for proprietary use - contact contact@osomi.net

## Contributing

We welcome contributions! Please see our [Contributing Guide](CONTRIBUTING.md) for details on:

- Setting up the development environment
- Code style guidelines
- Submitting pull requests
- Reporting issues

## Acknowledgments

- Built on [OxC3 (Oxsomi Core 3)](https://github.com/Oxsomi/core3)
- Developed by [Oxsomi](https://github.com/Oxsomi) / [Nielsbishere](https://github.com/Nielsbishere)
- Shader compilation powered by DirectX Shader Compiler (DXC)

## Support

- 📋 [Issues](https://github.com/Leahamckay/rt_core/issues) - Bug reports and feature requests
- 💬 [Discussions](https://github.com/Leahamckay/rt_core/discussions) - Community discussions
- 📧 contact@osomi.net - Commercial licensing inquiries