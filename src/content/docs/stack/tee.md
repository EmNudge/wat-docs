---
title: local.tee
description: Store a value into a local and keep it on the stack.
---

`local.tee` writes to a local variable and also leaves the value on the stack for further use.

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

There is no `global.tee` instruction. To set a global and keep the value on the stack, use `local.tee` into a temporary local and then `global.set`:

```wat
(module
  (global $g (mut i32) (i32.const 0))
  (func (param $x i32) (result i32)
    (local $tmp i32)
    local.get $x
    local.tee $tmp     ;; keep value on stack
    global.set $g      ;; store copy into global $g (pops)
    local.get $tmp     ;; push value back for further use
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
