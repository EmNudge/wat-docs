---
title: Reference Types
description: Using funcref and externref, with tables and ref.* instructions.
---

Reference types let Wasm refer to functions and host objects.

## Types

- `funcref`: reference to a function inside the module/table.
- `externref`: opaque reference to a host value (e.g., a JS object).

## ref.null, ref.func, ref.is_null

```wat
(module
  (type $t0 (func (param i32) (result i32)))
  (func $double (type $t0) (param $x i32) (result i32)
    local.get $x
    i32.const 2
    i32.mul)

  (table 2 funcref)
  (elem (i32.const 0) $double)

  (func (result i32)
    ref.null funcref       ;; push null funcref
    ref.is_null            ;; -> 1
  )

  (func (result i32)
    ref.func $double       ;; push a funcref to $double
    ref.is_null            ;; -> 0
  )
)
```

## Tables and call_indirect

```wat
(module
  (type $t0 (func (param i32) (result i32)))
  (func $double (type $t0) (param $x i32) (result i32)
    local.get $x
    i32.const 2
    i32.mul)
  (table 1 funcref)
  (elem (i32.const 0) $double)

  (func (param $n i32) (result i32)
    i32.const 0
    local.get $n
    call_indirect (type $t0))
)
```

## externref

From JS, you can pass host references as `externref` via imports or function parameters (supported environments only).

References:

- [Reference Instructions](/instructions/reference) - Complete reference for `ref.null`, `ref.func`, `ref.is_null`, `ref.as_non_null`
- [Table Instructions](/instructions/table) - `table.get`, `table.set`, `table.grow`, `table.fill`, etc.
- [Type Names](/instructions/types) - `funcref`, `externref`, and other reference types
- Spec: [Reference types and tables](https://webassembly.github.io/spec/core/syntax/index.html)
- Practice: function tables in [watlings](https://github.com/EmNudge/watlings/tree/main/exercises)
