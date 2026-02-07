---
title: "if / else"
description: Conditional execution with optional result values.
---


`if` consumes a condition (`i32`: 0 = false, non-zero = true). Both branches must match result types if present.

```wat
(module
  (func (param $x i32) (result i32)
    local.get $x
    i32.const 0
    i32.eq
    if (result i32)
      i32.const 1
    else
      i32.const 0
    end
  )
)
```

Patterns:

- Branchless value computation: use `if (result t)` to push a value from either branch.
- Omit `else` when not needed.

Further reading:

- [Control Flow Instructions](/instructions/control) - Complete reference for `block`, `loop`, `if`, `br`, `br_if`, etc.
- Spec: [If and block typing](https://webassembly.github.io/spec/core/syntax/index.html)
- Practice: conditionals in [watlings](https://github.com/EmNudge/watlings/tree/main/exercises)


