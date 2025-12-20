---
title: Types
description: Understand WAT value types, function signatures, locals, and results.
---

WAT’s type system is intentionally small. Most modules only need a handful of core types.

## Value types

Number types:

- `i32` and `i64`: 32-bit and 64-bit integers (signed/unsigned use the same type; the operator determines interpretation).
- `f32` and `f64`: 32-bit and 64-bit IEEE 754 floats.

Reference types (host references and function references):

- `funcref`: reference to a function.
- `externref`: an opaque reference to a host value (e.g., a JS object).

The spec tracks these in “Value Types” and “Reference Types.” See: [WebAssembly spec — Structure → Types](https://webassembly.github.io/spec/core/syntax/index.html).

## Function types

Functions declare parameter and result types. You can name parameters for readability.

```wat
(module
  ;; (func (param <types>...) (result <types>...)? ...)

  (func $add_i32 (param $a i32) (param $b i32) (result i32)
    local.get $a
    local.get $b
    i32.add)

  (func $mix (param $x i64) (param $y f32) (result f64)
    (local $acc f64)
    f64.const 0
    local.set $acc
    local.get $acc
    f64.convert_i64_s   ;; convert i64 -> f64
    local.get $y
    f64.promote_f32     ;; convert f32 -> f64
    f64.add)
)
```

Notes:

- Multiple results are supported: `(result i32 i64)` pushes two values.
- Use `local` to declare function-local variables. They must have a type.

## Blocks and block types

Control blocks (`block`, `loop`, `if`) can also declare result types, which affect the stack typing.

```wat
(module
  (func (param $n i32) (result i32)
    (block (result i32)
      local.get $n
      i32.const 0
      i32.eq
      if (result i32)
        i32.const 42     ;; if-branch result
      else
        i32.const 7      ;; else-branch result
      end
    )
  )
)
```

Both branches of an `if` with a result must produce the same typed value(s).

## Tables, memories, and globals (types overview)

- Tables: `funcref` or `externref` elements. Declared with limits, e.g., `(table 1 funcref)` or `(table 1 10 funcref)`.
- Memories: linear memory of bytes; typed by page limits (64 KiB per page), e.g., `(memory 1)` or `(memory 1 4)`.
- Globals: typed, optionally mutable values, e.g., `(global (mut i32) (i32.const 0))`.

```wat
(module
  (table $t 1 funcref)
  (memory $mem 1)
  (global $counter (mut i32) (i32.const 0))
)
```

For the formal grammar of all types, see the [WebAssembly spec — Structure → Types](https://webassembly.github.io/spec/core/syntax/index.html).

## Practice

If you learn best by doing, try the small, focused exercises in [watlings](https://github.com/EmNudge/watlings) and come back to this page as a quick reference.


