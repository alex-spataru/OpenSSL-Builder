# 🛠️ OpenSSL Builder (Static, Cross-Platform)

This repository builds **static OpenSSL libraries** for:

- ✅ **macOS (Universal: arm64 + x86_64)** via Clang
- ✅ **Windows (MSVC)** — native build on GitHub-hosted Windows runners
- ✅ **Windows (MinGW)** — cross-compiled from Linux using `mingw-w64`

These builds are **portable**, **redistributable**, and designed for integration into C++ projects that need a **fully self-contained OpenSSL setup** with no dynamic linking or runtime baggage.

Mostly built out of frustration. This repo was vibe-coded at 2 AM, while trying to get **MinGW builds of OpenSSL** without having access to a single Windows machine.

- If you're reading this and it works for you — you're welcome.
- If you're reading this and it doesn't — I'm sorry. PRs welcome.
  
## 🔄 Build Matrix

| Target Platform | Compiler | Strategy                      |
|-----------------|----------|-------------------------------|
| macOS           | Clang    | Dual-arch native (arm64/x86)  |
| Windows         | MSVC     | Native on Windows runner      |
| Windows         | MinGW    | Cross-compiled from Linux     |

Artifacts are uploaded automatically as part of a GitHub Release and include SHA256 checksums for verification.

## 📦 Output

Each build produces:
- Static `libssl.a` and `libcrypto.a`
- Matching OpenSSL headers
- Platform-specific layout (`lib`, `include`, etc.)
- SHA256 checksums in the release notes

You’ll find everything in the [Releases](../../releases) tab once a workflow completes.

## 📦 Output

Each workflow run builds and uploads the following:

```
openssl-out/
├── include/               # OpenSSL headers
└── lib/                   # Static libraries
├── libssl.a / .lib
└── libcrypto.a / .lib
```

### Example: Include in your project
```cmake
target_include_directories(MyApp PRIVATE path/to/openssl/include)
target_link_libraries(MyApp PRIVATE
  path/to/openssl/lib/libssl.a
  path/to/openssl/lib/libcrypto.a
)
```

For Windows with MSVC, use `.lib` files instead of `.a`.

## 🛡️ License

OpenSSL is licensed under Apache License 2.0.
This repo only builds the source — it doesn’t modify or redistribute it.
