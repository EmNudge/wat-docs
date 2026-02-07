---
title: Miscellaneous
description: Other instructions
---

## func.bind

Partially apply a function, binding some arguments to produce a new function reference with a reduced signature. This is part of the typed function references proposal and allows creating closures over function arguments.

**Signature:** `(param funcref args...) (result funcref)`

**Example:**

```wat
(type $binary (func (param i32 i32) (result i32)))
(type $unary (func (param i32) (result i32)))

;; Bind the first argument of an add function to create an "add 5" function
(func.bind (type $unary)
  (ref.func $add)      ;; function to partially apply
  (i32.const 5))       ;; bound first argument
```

---
