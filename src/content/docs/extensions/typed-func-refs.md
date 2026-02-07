---
title: "Typed Function References"
description: "Precise typing for function references and call_ref."
---


Typed function references make function refs carry specific types and enable `call_ref`.

```wat
(module
  (type $t0 (func (param i32) (result i32)))
  (func $inc (type $t0) (param $x i32) (result i32)
    local.get $x
    i32.const 1
    i32.add)
  (table 1 funcref)
  (elem (i32.const 0) $inc)

  (func (export "dispatch") (param $i i32) (param $x i32) (result i32)
    local.get $i
    ref.func $inc
    drop                  ;; example only; normally fetch from table
    local.get $x
    call_ref (type $t0))
)
```

References:

- [Control Flow Instructions](/instructions/control) - `call_ref`, `return_call_ref`, `br_on_null`, `br_on_non_null`
- [Reference Instructions](/instructions/reference) - `ref.func`, `ref.null`, `ref.is_null`, `ref.as_non_null`
- Spec: https://webassembly.github.io/spec/core/syntax/index.html
- Practice: dispatch patterns in https://github.com/EmNudge/watlings


