---
title: tee (local.tee / global.tee)
description: Store a value and keep it on the stack.
---


`tee` variants write to a variable and also leave the value on the stack for further use.

## local.tee

```wat
(module
  (func (param $x i32) (result i32)
    (local $y i32)
    local.get $x
    local.tee $y       ;; store into $y, keep value on stack
    i32.const 1
    i32.add)           ;; result = $y + 1
)
```

## global.tee

```wat
(module
  (global $g (mut i32) (i32.const 0))
  (func (param $x i32) (result i32)
    local.get $x
    global.tee $g      ;; store into global $g, keep value on stack
    i32.const 2
    i32.mul)
)
```

Use cases:

- Avoid repeating `local.get` when you need both to store and to continue processing.
- Pipeline-style computations where an intermediate is also the final result.

References:

- [Local & Global Instructions](/instructions/local-global) - Complete reference for `local.get`, `local.set`, `local.tee`, `global.get`, `global.set`
- Spec: [Variable instructions — tee](https://webassembly.github.io/spec/core/syntax/index.html)
- Practice: variable ops in [watlings](https://github.com/EmNudge/watlings/tree/main/exercises)


