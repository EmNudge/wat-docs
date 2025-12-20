---
title: "Garbage Collection (WasmGC)"
description: "Low-level primitives for managed structs/arrays to support GC languages."
---

WasmGC provides reference-typed objects (structs, arrays) that engines can manage with garbage collection. This enables efficient runtimes for languages like Kotlin/Java/Dart.

Concepts:

- Reference-typed heaps managed by the VM.
- Typed `struct` and `array` values.
- Interop with host via `externref`.

Because syntax and support are evolving, check your toolchain’s documentation for exact WAT forms. Explore language toolchains that target WasmGC for real-world usage.

References:

- Spec overview (evolving proposals): https://webassembly.github.io/spec/core/syntax/index.html
- Practice: higher-level runtimes often showcased outside of watlings, but see https://github.com/EmNudge/watlings for fundamentals


