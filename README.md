# 🛠️ OpenSSL Builder (Static, Cross-Platform)

This repository builds **static OpenSSL libraries** for:

- ✅ **Windows (MinGW)**
- ✅ **Windows (MSVC)**
- ✅ **macOS (Clang)**

The output is portable, redistributable, and suitable for embedding in C++ projects that require a fully self-contained OpenSSL setup.

## 📦 Output

Each workflow run builds and uploads the following:

```
openssl-out/
├── include/               # OpenSSL headers
└── lib/                   # Static libraries
├── libssl.a / .lib
└── libcrypto.a / .lib
```

## 🧱 Build Matrix

| Platform        | Toolchain       | Target Triplet       | Output Format |
|----------------|------------------|-----------------------|----------------|
| Windows         | MinGW            | `mingw64`             | `.a` (GCC)     |
| Windows         | MSVC             | `VC-WIN64A`           | `.lib` (MSVC)  |
| macOS           | Clang (native)   | `darwin64-x86_64-cc`  | `.a` (Clang)   |

## 🚀 Usage

You can manually trigger a build from the **Actions** tab or clone and build locally.

### Example: Include in your project
```cmake
target_include_directories(MyApp PRIVATE path/to/openssl/include)
target_link_libraries(MyApp PRIVATE
  path/to/openssl/lib/libssl.a
  path/to/openssl/lib/libcrypto.a
)
```

For Windows with MSVC, use `.lib` files instead of `.a`.

## 📁 Artifacts

CI builds will upload artifacts you can download directly from the GitHub Actions UI, or wire into your own project as a cache.

## 🛡️ License

OpenSSL is licensed under Apache License 2.0.
This repo only builds the source — it doesn’t modify or redistribute it.
