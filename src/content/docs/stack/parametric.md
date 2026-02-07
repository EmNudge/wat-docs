---
title: Parametric Instructions
description: "Stack-level utilities: drop and select for branchless control."
---


Parametric instructions operate directly on the value stack. They’re simple but powerful for branchless logic and cleanup.

## drop

Pop and discard the top stack value.

```wat
(module
  (func (param $x i32) (result i32)
    i32.const 123
    drop               ;; discard
    local.get $x       ;; the remaining value to return
  )
)
```

Use cases:

- Ignore an unused result (e.g., when an instruction produces an extra value).
- Clean up the stack before producing a block result.

## select

Choose between two values based on an `i32` condition (`0` = false):

```wat
(module
  (func (param $a i32) (param $b i32) (param $cond i32) (result i32)
    local.get $a
    local.get $b
    local.get $cond
    select)
)
```

Notes:

- Both candidate values must have the same type.
- Some toolchains support typed `select` forms; consult your assembler.

Further reading:

- [Parametric Instructions](/instructions/parametric) - Complete reference for `drop`, `select`
- Spec: [Parametric instructions](https://webassembly.github.io/spec/core/syntax/index.html)
- Practice: related exercises in [watlings](https://github.com/EmNudge/watlings/tree/main/exercises)


