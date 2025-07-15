# Contributing to RT Core

Thank you for your interest in contributing to RT Core! This document provides guidelines and information for contributing to this raytracing framework built on OxC3 (Oxsomi Core 3).

## Table of Contents

- [Getting Started](#getting-started)
- [Development Environment Setup](#development-environment-setup)
- [Building the Project](#building-the-project)
- [Testing](#testing)
- [Code Style Guidelines](#code-style-guidelines)
- [Contributing Process](#contributing-process)
- [License Information](#license-information)
- [Getting Help](#getting-help)

## Getting Started

RT Core is a raytracing framework that provides abstractions for raytracing applications built on top of OxC3 (Oxsomi Core 3). The project supports:

- Cross-platform development (Windows, Linux, macOS, Android, iOS)
- Multiple graphics APIs (Vulkan, D3D12, Metal)
- Raytracing pipelines and inline raytracing
- Modern C/C++ with SIMD optimizations
- Shader compilation and resource management

## Development Environment Setup

### Prerequisites

1. **Build Tools:**
   - CMake 3.13.0 or later
   - Conan package manager (version 2.0+)
   - Git with submodule support

2. **Compilers:**
   - **Windows:** Visual Studio 2022 (MSVC 194+) with C++20 support
   - **Linux/macOS:** GCC or Clang with C++20 support
   - **Android:** Android NDK

3. **Graphics Drivers:**
   - Vulkan-capable drivers (recommended)
   - DirectX 12 capable drivers (Windows)

### Initial Setup

1. Clone the repository with submodules:
   ```bash
   git clone --recursive https://github.com/Leahamckay/rt_core.git
   cd rt_core
   ```

2. If you've already cloned without submodules:
   ```bash
   git submodule update --init --recursive
   ```

3. Install Conan dependencies (this will be handled by the build scripts)

## Building the Project

### Windows

Use the provided batch script:

```cmd
build.bat [Debug|Release|RelWithDebInfo] [True|False] [True|False] [True|False] [True|False]
```

Parameters:
1. Build type: `Debug`, `Release`, or `RelWithDebInfo`
2. Enable SIMD: `True` or `False`
3. Force Vulkan: `True` or `False`
4. In-repo compile: `True` or `False`
5. Dynamic linking: `True` or `False`

Example:
```cmd
build.bat Debug True False False False
```

### Linux/macOS

Use the provided shell script:

```bash
./build.sh [Debug|Release] [True|False] [True|False] [True|False] [True|False]
```

Parameters:
1. Build type: `Debug` or `Release`
2. Enable SIMD: `True` or `False`
3. Force Vulkan: `True` or `False`
4. In-repo compile: `True` or `False`
5. Dynamic linking: `True` or `False`

Example:
```bash
./build.sh Debug True False False False
```

### Android

Use the Python build script:

```bash
python build_android.py
```

### Manual Building with Conan

If you prefer manual building:

```bash
# Install dependencies
conan install . -s build_type=Debug --build=missing

# Build
conan build .
```

## Testing

The project includes test infrastructure in the `tst/` directory:

- `test.c` - Main test application demonstrating raytracing features
- `atmos_helper.c/h` - Atmospheric rendering helper functions

### Running Tests

After building, run the test application:

- **Windows:** `build/Debug/windows/x64/bin/rt_core.exe`
- **Linux:** `build/Debug/linux/x64/bin/rt_core`

### Test Controls

The test application supports keyboard controls:
- **F2:** Toggle keyboard visibility
- **F9:** Pause/unpause rendering
- **F10:** Spawn additional windows (desktop only)
- **F11:** Toggle fullscreen
- **WASD/Arrow Keys:** Camera movement
- **Q/E:** Vertical movement
- **Shift:** Faster movement

## Code Style Guidelines

### C/C++ Code Style

1. **Naming Conventions:**
   - Types: `PascalCase` (e.g., `TestWindowManager`)
   - Functions: `PascalCase` with module prefix (e.g., `GraphicsDevice_create`)
   - Variables: `camelCase` (e.g., `framesSinceLastSecond`)
   - Constants: `UPPER_SNAKE_CASE` (e.g., `KIBI`)
   - Enums: `EPrefixedPascalCase` (e.g., `EGraphicsApi_Vulkan`)

2. **Code Organization:**
   - Use consistent indentation (tabs preferred)
   - Keep functions focused and reasonably sized
   - Add error handling with the `gotoIfError` pattern
   - Use the project's reference counting system for resource management

3. **Memory Management:**
   - Follow the project's reference counting patterns
   - Use the `_dec` and `_inc` functions for resource management
   - Clean up resources in reverse order of creation

4. **Error Handling:**
   - Use the project's error handling macros (`gotoIfError2`, `gotoIfError3`)
   - Provide meaningful error messages
   - Clean up resources on error paths

### Shader Code

- Use HLSL with Oxsomi's shader extensions (.oiSH files)
- Place shaders in the `res/shaders/` directory
- Follow consistent naming for shader entry points (`main`, `mainVS`, `mainPS`, etc.)

## Contributing Process

### Before You Start

1. Check existing issues and pull requests to avoid duplicates
2. For major changes, create an issue to discuss the proposal first
3. Ensure you understand the project's architecture and goals

### Making Changes

1. **Fork and Branch:**
   ```bash
   git checkout -b feature/your-feature-name
   ```

2. **Make Your Changes:**
   - Follow the code style guidelines
   - Add tests if applicable
   - Update documentation as needed
   - Ensure your code builds on your target platform(s)

3. **Test Your Changes:**
   - Build and test on your platform
   - Verify no regressions in existing functionality
   - Test with different build configurations if possible

4. **Commit Your Changes:**
   - Use clear, descriptive commit messages
   - Follow conventional commit format if possible
   - Keep commits atomic and logical

### Submitting Pull Requests

1. **Create a Pull Request:**
   - Provide a clear title and description
   - Reference any related issues
   - Explain the motivation and approach
   - Include screenshots/videos for visual changes

2. **Pull Request Requirements:**
   - All builds must pass
   - Code follows project style guidelines
   - New features include appropriate tests
   - Documentation is updated if needed

3. **Review Process:**
   - Maintainers will review your changes
   - Address feedback promptly
   - Be prepared to iterate on your changes

### Types of Contributions

We welcome various types of contributions:

- **Bug Fixes:** Clear reproduction steps and targeted fixes
- **Features:** New raytracing capabilities, platform support, optimizations
- **Documentation:** Improvements to guides, API documentation, examples
- **Testing:** Additional test cases, platform testing, performance benchmarks
- **Build System:** Improvements to CMake, Conan, or build scripts

## License Information

### Dual Licensing

RT Core is dual-licensed under:

1. **GNU General Public License v3.0 (GPL-3.0)** - For open source projects
2. **Commercial License** - For proprietary/commercial projects

### Important License Considerations

- **GPL-3.0 Requirements:** If you distribute RT Core or a derivative work publicly, your project must also be GPL-3.0 licensed
- **Commercial License:** For proprietary use, contact contact@osomi.net for commercial licensing options
- **Contributor License:** By contributing, you agree that your contributions will be licensed under the same dual license terms

### Contributing Code

- Ensure you have the right to contribute your code
- Original code only - no copyrighted material from other projects
- By submitting a pull request, you agree to license your contribution under the project's dual license

## Getting Help

### Resources

- **Documentation:** Check existing documentation and code comments
- **Issues:** Search existing issues for solutions or similar problems
- **Examples:** Study the test application in `tst/test.c` for usage patterns

### Support Channels

- **GitHub Issues:** For bugs, feature requests, and general questions
- **Pull Request Discussions:** For code review and implementation discussions

### Reporting Issues

When reporting issues, please include:

1. **Environment Information:**
   - Operating system and version
   - Graphics hardware and drivers
   - Build configuration used
   - Compiler version

2. **Reproduction Steps:**
   - Clear steps to reproduce the issue
   - Expected vs. actual behavior
   - Any error messages or logs

3. **Additional Context:**
   - Screenshots or videos if applicable
   - Minimal code example demonstrating the issue
   - Any workarounds you've discovered

## Platform-Specific Considerations

### Windows
- Requires Visual Studio 2022 or later
- DirectX 12 and Vulkan support available
- Use the provided `.bat` build script

### Linux
- Requires recent GCC or Clang
- Vulkan support required
- Additional dependencies may be needed (check build script)

### macOS
- Metal and Vulkan (via MoltenVK) support
- Xcode command line tools required

### Android
- Uses Android NDK
- Vulkan support on compatible devices
- Use the Python build script

### iOS
- Metal support
- Xcode required for building

---

Thank you for contributing to RT Core! Your contributions help advance real-time raytracing technology and benefit the entire community.