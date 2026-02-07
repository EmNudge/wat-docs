---
title: Float Unary Ops
description: abs, neg, sqrt, ceil, floor, trunc, nearest, min, max, copysign.
---


```wat
(module
  (func (export "rounding") (param $x f32) (result f32)
    local.get $x
    f32.ceil)               ;; f32.floor, f32.trunc, f32.nearest
)
```

Other float unary ops:

- `f32.abs`, `f32.neg`, `f32.sqrt`
- `f32.min`, `f32.max`, `f32.copysign`
- All available as `f64.*` too

Reference:
- [f32 Instructions](/instructions/f32) - Complete f32 instruction reference
- [f64 Instructions](/instructions/f64) - Complete f64 instruction reference
- Spec: https://webassembly.github.io/spec/core/syntax/index.html
- Practice: float ops in https://github.com/EmNudge/watlings


