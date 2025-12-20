---
title: "Memory & Data"
description: Linear memory, loads/stores, memory size/grow, and data segments.
---

WebAssembly exposes a contiguous byte array called linear memory. You interact with it using typed load/store instructions and can initialize it using data segments.

## Declaring and exporting memory

```wat
(module
  (memory $mem 1 4)            ;; min 1 page (64 KiB), max 4
  (export "memory" (memory $mem))
)
```

## Loads and stores

Typed operations read/write values at byte offsets. Narrow variants sign/zero-extend on load and truncate on store.

```wat
(module
  (memory 1)
  (func (param $ptr i32) (result i32)
    i32.const 0x7F
    local.get $ptr
    i32.store8            ;; store one byte
    local.get $ptr
    i32.load8_u)          ;; zero-extend back to i32
)
```

Common ops:

- Loads: `i32.load`, `i64.load`, `f32.load`, `f64.load`, `i32.load8_s`, `i32.load8_u`, `i32.load16_s`, `i32.load16_u`, …
- Stores: `i32.store`, `i64.store`, `f32.store`, `f64.store`, `i32.store8`, `i32.store16`, …

## memory.size and memory.grow

```wat
(module
  (memory 1)
  (func (result i32)
    memory.size          ;; pages
  )
  (func (param $pages i32) (result i32)
    local.get $pages
    memory.grow          ;; returns old size, or -1 on failure
  )
)
```

If memory grows, the underlying ArrayBuffer can change; recreate typed array views on the host.

## Data segments

```wat
(module
  (memory 1)
  (data (i32.const 0) "Hi")
)
```

You can use `(offset ...)` inside passive segments with bulk memory ops in advanced scenarios.

References:

- Spec: [Memories and data segments](https://webassembly.github.io/spec/core/syntax/index.html)
- Practice: memory tasks in [watlings](https://github.com/EmNudge/watlings/tree/main/exercises)


