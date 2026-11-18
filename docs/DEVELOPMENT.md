# Development

Nemunemu uses C17 for ordinary Linux and Linux-WASM userspace builds.
The pinned Thistle checkout supplies opcode and syscall definitions.
Regenerate the ABI header after changing that pin:

```sh
python3 scripts/generate-abi.py
python3 scripts/generate-abi.py --check
```

Build and test the native runtime:

```sh
cmake -S . -B build
cmake --build build --parallel 2
ctest --test-dir build --output-on-failure
```

Run the address and undefined-behaviour sanitiser checks for changes to
parsing, memory or execution.
