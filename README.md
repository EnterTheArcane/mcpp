# mcpp

A minimal [mcpp 2.7.2](https://sourceforge.net/projects/mcpp/files/mcpp/V.2.7.2/) C/C++ preprocessor library by Kiyoshi Matsui, used to preprocess O3DE's AZSL shaders. Sources include [O3DE's existing patches](https://github.com/o3de/3p-package-source/blob/70f0b7b5257bf7cf935bf1cfd270e1b53ccead18/package-system/mcpp/mcpp_2.7.2_az.patch) and some portability changes.

Changes for O3DE:

- C++ linkage, const arguments, prefixed output names, and an include callback.
- Absolute paths in line directives, Windows path handling, and preserved comment line numbers for shader diagnostics.
- Windows, Mac, and Linux configuration, ARM64 detection, lowercase headers, and modern compiler fixes.

```sh
cmake -S . -B build -DCMAKE_BUILD_TYPE=Release
cmake --build build --config Release
```

Upstream mcpp uses [BSD-2-Clause](LICENSE.txt). O3DE modifications and build files use [Apache-2.0](LICENSE_APACHE2.txt) OR [MIT](LICENSE_MIT.txt), at your option. The upstream license still applies to the original code.
