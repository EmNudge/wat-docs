---
title: "Bulk Memory Operations"
description: "Efficient copying and filling for memory and tables."
---

Bulk memory adds fast, in-engine operations for copying/filling regions of memory and tables.

## memory.copy and memory.fill

```wat
(module
  (memory (export "memory") 1)
  (func (export "copy") (param $dst i32) (param $src i32) (param $len i32)
    local.get $dst
    local.get $src
    local.get $len
    memory.copy)
  (func (export "fill") (param $dst i32) (param $value i32) (param $len i32)
    local.get $dst
    local.get $value
    local.get $len
    memory.fill)
)
```

## table.copy, table.fill

```wat
(module
  (table (export "table") 10 funcref)
  (func (export "tfill") (param $idx i32) (param $len i32)
    ref.null funcref
    local.get $idx
    local.get $len
    table.fill)
)
```

References:

- Spec: https://webassembly.github.io/spec/core/syntax/index.html
- Practice: memory/table tasks in https://github.com/EmNudge/watlings


