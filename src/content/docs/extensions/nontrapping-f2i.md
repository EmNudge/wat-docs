---
title: "Non-trapping float-to-int"
description: "Saturating conversions from floats to integers that do not trap."
---

Instead of trapping on overflow/NaN, these instructions clamp to min/max and convert NaN to 0.

```wat
(module
  (func (export "sat") (param $x f32) (result i32)
    local.get $x
    i32.trunc_sat_f32_s)
)
```

Variations include:

- `i32.trunc_sat_f32_s`, `i32.trunc_sat_f32_u`, `i32.trunc_sat_f64_s`, `i32.trunc_sat_f64_u`
- `i64.trunc_sat_f32_s`, `i64.trunc_sat_f32_u`, `i64.trunc_sat_f64_s`, `i64.trunc_sat_f64_u`

References:

- Spec: https://webassembly.github.io/spec/core/syntax/index.html
- Practice: numeric conversions in https://github.com/EmNudge/watlings


