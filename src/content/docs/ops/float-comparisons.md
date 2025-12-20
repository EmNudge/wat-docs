---
title: Float Comparisons
description: f32/f64 eq, ne, lt/le/gt/ge with NaN semantics.
---

Float comparisons push `i32` booleans. NaN makes `eq` false and `ne` true; comparisons with NaN are false.

```wat
(module
  (func (export "fcmp") (param $x f32) (param $y f32) (result i32)
    local.get $x
    local.get $y
    f32.le)                 ;; f32.eq, f32.ne, f32.lt, f32.le, f32.gt, f32.ge; f64.* variants
)
```

Reference:
- Spec: https://webassembly.github.io/spec/core/syntax/index.html
- Practice: comparisons in https://github.com/EmNudge/watlings


