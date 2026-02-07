---
title: "call & call_indirect"
description: Direct calls to known functions and indirect calls via tables.
---


`call` invokes a known function by index/name. `call_indirect` dispatches through a table and type-checks a function signature at runtime.

```wat
(module
  (type $t0 (func (param i32) (result i32)))

  (func $double (type $t0) (param $x i32) (result i32)
    local.get $x
    i32.const 2
    i32.mul)

  (func (export "use_call") (param $n i32) (result i32)
    local.get $n
    call $double)

  (table 1 funcref)
  (elem (i32.const 0) $double)

  (func (export "use_call_indirect") (param $n i32) (result i32)
    i32.const 0
    local.get $n
    call_indirect (type $t0))
)
```

Notes:

- `call_indirect` takes a table index then the call arguments.
- The function referenced must match the declared `(type ...)`, or the call traps.

Further reading:

- [Control Flow Instructions](/instructions/control) - Complete reference for `call`, `call_indirect`, `call_ref`, etc.
- [Table Instructions](/instructions/table) - `table.get`, `table.set`, `table.grow`, etc.
- Spec: [Call instructions, tables, and types](https://webassembly.github.io/spec/core/syntax/index.html)
- Practice: function dispatch patterns in [watlings](https://github.com/EmNudge/watlings/tree/main/exercises)


