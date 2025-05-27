<img height="128px" src="https://upload.wikimedia.org/wikipedia/commons/6/6a/OpenSSL_logo.svg"/>

[![CI Build](https://github.com/alex-spataru/OpenSSL-Builder/actions/workflows/build.yml/badge.svg)](https://github.com/alex-spataru/OpenSSL-Builder/actions/workflows/build.yml)

This repository automates the process of building **static OpenSSL libraries** for multiple platforms. It is intended for C++ developers who need portable, redistributable OpenSSL binaries without relying on shared libraries or dynamic runtime dependencies.

## Supported Targets

- **macOS (Universal)**  
  Built natively for both `arm64` and `x86_64` using Clang and merged using `lipo`.

- **Windows (MSVC)**  
  Built natively using Microsoft's Visual Studio toolchain on GitHub-hosted Windows runners.

- **Windows (MinGW)**  
  Cross-compiled from Linux using `mingw-w64` targeting Windows.

All builds are self-contained and do not require OpenSSL to be installed on the target system.

## Build Strategy

| Target Platform | Compiler | Build Strategy                    |
|-----------------|----------|-----------------------------------|
| macOS           | Clang    | Dual-arch native (arm64 + x86_64) |
| Windows         | MSVC     | Native build with `nmake`         |
| Windows         | MinGW    | Cross-compiled from Ubuntu        |

## Output Structure

Each completed build produces the following output:

```
openssl-out/
├── include/              
├── lib/                   
├──── libssl.a / libssl.lib
├──── libcrypto.a / libcrypto.lib
└── LICENSE-OpenSSL.txt
```

## How to Use

Integrating OpenSSL in a CMake-based project typically looks like this:

```cmake
target_include_directories(MyApp PRIVATE path/to/openssl/include)
target_link_libraries(MyApp PRIVATE
  path/to/openssl/lib/libssl.a
  path/to/openssl/lib/libcrypto.a
)
```

> On Windows with MSVC, use `.lib` files. On MinGW/macOS, use `.a`.

## Artifact Delivery

Each build run automatically uploads precompiled binaries as GitHub Actions artifacts or release assets. SHA256 checksums are included to validate integrity.

You can retrieve the latest prebuilt outputs from the [Releases](../../releases) page.

## License

This repository does **not** modify or redistribute OpenSSL source code.  
It uses the official sources available at [openssl.org](https://www.openssl.org/source/), built as-is.

OpenSSL is licensed under the [Apache License 2.0](https://www.openssl.org/source/license-openssl-ssleay.txt).
