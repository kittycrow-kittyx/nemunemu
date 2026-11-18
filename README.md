# NEMUNEMU

**NEMUNEMU**: NEMUnemu is Not an EMUlator.

Nemunemu is a Linux userspace runtime for THX1 and THX2 executables. It
interprets guest instructions, translates the guest syscall ABI and handles
`#!thistle:<command>` and THX wrapper scripts. It can run as Linux init.

## Native build and test

```sh
git submodule update --init --recursive
cmake -S . -B build
cmake --build build --parallel 2
ctest --test-dir build --output-on-failure
```

## Linux-WASM build

Requires a Linux-WASM checkout with its LLVM toolchain, musl sysroot and
kernel headers installed in the selected workspace.

```sh
LINUX_WASM_ROOT=/path/to/linux-wasm \
LW_WORKSPACE=/path/to/linux-wasm/workspace \
  ./scripts/build-linux-wasm.sh
```

The default output is `dist/nemunemu-wasm32_nommu.wasm`. Install it at
`/sbin/nemunemu` in a root filesystem when using Neru's default init path.

## Runtime modes

```text
nemunemu --shell ROOT
nemunemu --marker SCRIPT [ARG ...]
nemunemu --thx-wrapper SCRIPT [ARG ...]
nemunemu --image PROGRAMME.thx [-- ARG ...]
```

See [architecture](docs/ARCHITECTURE.md) and [development](docs/DEVELOPMENT.md).

## Licence

[MIT](LICENSE).
