# dxc-build

Automated cross-platform builds of [microsoft/DirectXShaderCompiler](https://github.com/microsoft/DirectXShaderCompiler) with SPIR-V codegen enabled.

A GitHub Actions workflow checks daily for new upstream tags and, when one appears, builds DXC for Windows, Linux, and macOS, then publishes a combined archive as a GitHub Release.

## Releases

See the [Releases page](../../releases) for prebuilt binaries.

Each release contains a single `dxc-<tag>.zip` with the following layout:

```
dxc-<tag>/
├── windows-x86_64/
│   ├── bin/
│   │   ├── dxc.exe
│   │   └── dxcompiler.dll
│   ├── lib/dxcompiler.lib
│   └── include/dxc/
├── linux-x86_64/
│   ├── bin/dxc
│   ├── lib/libdxcompiler.so
│   └── include/dxc/
└── macos-arm64/
    ├── bin/dxc
    ├── lib/libdxcompiler.dylib
    └── include/dxc/
```

## Features

- **SPIR-V codegen enabled** — all binaries support the `-spirv` flag for Vulkan/Metal workflows.
- **Official build mode** (`HLSL_OFFICIAL_BUILD=ON`).
- Tests and `dxilconv` are disabled to keep build times down.

## Notes

- As of the [February 2025 DXC release](https://github.com/microsoft/DirectXShaderCompiler/releases/tag/v1.8.2502), Microsoft open-sourced the DXIL validator hash, so shader validation and signing now run natively in-process on all platforms, with no dependency on the proprietary `dxil.dll`/`libdxil.so` blob.
- Builds are triggered automatically by `.github/workflows/build.yml` on a daily schedule, and can also be run manually via the Actions tab.

## License

DirectXShaderCompiler is licensed under the [University of Illinois/NCSA Open Source License](https://github.com/microsoft/DirectXShaderCompiler/blob/main/LICENSE.TXT). This repository only contains build automation; all binaries are built directly from upstream sources.
