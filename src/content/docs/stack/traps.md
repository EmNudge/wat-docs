---
title: Traps
description: When and how execution traps (errors) occur in WebAssembly.
---


A trap is a runtime error that aborts execution. Common trap sources include:

- `unreachable` executed
- Division by zero (integer)
- Integer overflow on signed division `i32.div_s` with `INT_MIN / -1`
- Invalid `call_indirect` type mismatch or out-of-bounds table index
- Out-of-bounds memory access

## unreachable

```wat
(module
  (func (param $x i32)
    local.get $x
    i32.const 0
    i32.lt_s
    if
      unreachable        ;; will trap if executed
    end
  )
)
```

## Memory OOB

```wat
(module
  (memory 1)
  (func
    i32.const 70000      ;; > 64 KiB (one page)
    i32.load             ;; will trap if address out of bounds
  )
)
```

## call_indirect mismatch

```wat
(module
  (type $t0 (func (param i32) (result i32)))
  (func $f0 (type $t0) (param $x i32) (result i32)
    local.get $x)
  (table 1 funcref)
  (elem (i32.const 0) $f0)
  (func (param $x i32) (result i32)
    i32.const 0
    local.get $x
    call_indirect (type $t0))   ;; OK; any mismatch here would trap
)
```

References:

- [Control Flow Instructions](/instructions/control) - `unreachable`, `call_indirect`, etc.
- [i32 Instructions](/instructions/i32) - `i32.div_s`, `i32.load`, `i32.store`, etc.
- Spec: [Runtime — Traps](https://webassembly.github.io/spec/core/syntax/index.html)
- Practice: defensive coding in [watlings](https://github.com/EmNudge/watlings/tree/main/exercises)


