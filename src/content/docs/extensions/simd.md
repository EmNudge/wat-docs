---
title: 'Fixed-width SIMD (128-bit)'
description: 'Vector operations with v128 values and lane-wise instructions.'
---

SIMD enables lane-wise parallel operations on 128-bit vectors.

```wat
(module
  (func (export "add4") (param $x v128) (param $y v128) (result v128)
    local.get $x
    local.get $y
    i32x4.add)
)
```

Notes:

- Construct vectors with `v128.const`, `i32x4.splat`, etc.
- Load/store with `v128.load` / `v128.store`. Requires appropriate alignment/feature support.

References:

- [SIMD Instructions](/instructions/simd) - Complete reference for all v128, i8x16, i16x8, i32x4, i64x2, f32x4, f64x2 operations
- Spec: https://webassembly.github.io/spec/core/syntax/index.html
- Practice: numeric fundamentals in https://github.com/EmNudge/watlings
