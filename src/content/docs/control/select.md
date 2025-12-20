---
title: select
description: Choose between two stack values based on an i32 condition.
---

`select` pops three values: `a`, `b`, and a condition `c`. It pushes `a` if `c != 0`, else `b`. Both `a` and `b` must share the same type.

```wat
(module
  (func (param $x i32) (param $y i32) (param $cond i32) (result i32)
    local.get $x
    local.get $y
    local.get $cond
    select)
)
```

Typed `select` (in newer specs) lets you annotate the result type; in WAT this may appear as `select (result i32)` depending on toolchain support.

Use cases:

- Branchless min/max building blocks.
- Compact conditional expressions without `if`.

Further reading:

- Spec: [Parametric select](https://webassembly.github.io/spec/core/syntax/index.html)
- Practice: try conditional computations in [watlings](https://github.com/EmNudge/watlings/tree/main/exercises)


