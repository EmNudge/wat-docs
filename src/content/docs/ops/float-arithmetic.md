---
title: Float Arithmetic
description: f32/f64 add, sub, mul, div with IEEE 754 semantics.
---


```wat
(module
  (func (export "fops") (param $x f64) (param $y f64) (result f64)
    local.get $x
    local.get $y
    f64.mul)                ;; f32.add, f32.sub, f32.mul, f32.div; f64.* variants
)
```

Floats follow IEEE 754: NaNs propagate; division by zero yields ±Inf (no trap).

Reference:
- [f32 Instructions](/instructions/f32) - Complete f32 instruction reference
- [f64 Instructions](/instructions/f64) - Complete f64 instruction reference
- Spec: https://webassembly.github.io/spec/core/syntax/index.html
- Practice: floats in https://github.com/EmNudge/watlings


