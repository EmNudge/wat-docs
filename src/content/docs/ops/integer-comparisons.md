---
title: Integer Comparisons
description: eq, ne, lt/le/gt/ge with signed/unsigned variants.
---

Comparisons push `i32` booleans (0 = false, 1 = true).

```wat
(module
  (func (export "cmp") (param $x i32) (param $y i32) (result i32)
    local.get $x
    local.get $y
    i32.lt_s)               ;; i32.lt_u, i32.le_s/u, i32.gt_s/u, i32.ge_s/u, i32.eq, i32.ne
)
```

- Signed ops: `lt_s`, `le_s`, `gt_s`, `ge_s`
- Unsigned ops: `lt_u`, `le_u`, `gt_u`, `ge_u`
- Equality ops: `eq`, `ne`
- 64-bit variants: `i64.*`

Reference:
- Spec: https://webassembly.github.io/spec/core/syntax/index.html
- Practice: comparisons in https://github.com/EmNudge/watlings


