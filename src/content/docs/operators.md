---
title: Operators
description: The essential WAT instructions for arithmetic, comparison, locals, and control flow.
---

At its core, WebAssembly is a stack machine. Most instructions pop their operands from the stack and push results back. Below are the operators you’ll reach for most often.

For full instruction lists and exact rules, see the [WebAssembly spec — Structure → Instructions](https://webassembly.github.io/spec/core/syntax/index.html).

## Reading and writing locals

```wat
(func (param $a i32) (param $b i32) (result i32)
  (local $tmp i32)
  local.get $a       ;; push a
  local.get $b       ;; push b
  i32.add            ;; pop a,b -> push (a+b)
  local.set $tmp     ;; store result into $tmp (pops)
  local.get $tmp     ;; push $tmp again
)
```

- `local.get $x`: push the value of local `$x`.
- `local.set $x`: pop and store into local `$x`.
- `local.tee $x`: like set, but also re-pushes the stored value.

## Numeric arithmetic

Integer arithmetic (wraps on overflow):

```wat
(func (param $x i32) (param $y i32) (result i32)
  local.get $x
  local.get $y
  i32.add)     ;; i32.sub, i32.mul, i32.div_s, i32.div_u, i32.rem_s, i32.rem_u
```

Float arithmetic:

```wat
(func (param $x f64) (param $y f64) (result f64)
  local.get $x
  local.get $y
  f64.mul)     ;; f32.add, f32.sub, f32.mul, f32.div; f64.* variants
```

Bitwise and shifts (integers only):

```wat
(func (param $x i32) (param $y i32) (result i32)
  local.get $x
  local.get $y
  i32.and)     ;; i32.or, i32.xor, i32.shl, i32.shr_s, i32.shr_u, i32.rotl, i32.rotr
```

## Comparisons

Comparisons push `i32` booleans (0 = false, 1 = true).

```wat
(func (param $x i64) (param $y i64) (result i32)
  local.get $x
  local.get $y
  i64.lt_s)    ;; i64.eq, i64.ne, i64.lt_s/u, i64.le_s/u, i64.gt_s/u, i64.ge_s/u
```

Floats use IEEE 754 semantics (NaN-aware):

```wat
(func (param $x f32) (param $y f32) (result i32)
  local.get $x
  local.get $y
  f32.eq)      ;; f32.ne, f32.lt, f32.le, f32.gt, f32.ge; f64.* variants
```

## Conversions

Common conversions:

```wat
(func (param $x i32) (param $y f32) (result f64)
  local.get $x
  f64.convert_i32_s   ;; signed i32 -> f64
  local.get $y
  f64.promote_f32     ;; f32 -> f64
  f64.add)
```

Other families include `extend`/`wrap` between integer widths and `trunc` from floats to ints (with `_s` or `_u` variants).

## Control flow: block, loop, if

```wat
(func (param $n i32) (result i32)
  (local $acc i32)
  i32.const 0
  local.set $acc
  (loop $again
    local.get $n
    i32.eqz
    br_if $done          ;; if n == 0 -> break to $done
    local.get $acc
    i32.const 1
    i32.add
    local.set $acc
    local.get $n
    i32.const 1
    i32.sub
    local.set $n
    br $again
  )
  (block $done)
  local.get $acc)
```

Notes:

- `block` introduces a label you can `br`eak to (exits the block).
- `loop` runs its body and treats `br` as a continue (jumps to top).
- `br_if $label` pops a condition; branch if non-zero.

See the spec for precise typing rules and structured control forms: [WebAssembly spec — Instructions](https://webassembly.github.io/spec/core/syntax/index.html).

## Instruction Reference

For complete instruction documentation with signatures and examples:

- [i32 Instructions](/instructions/i32) - All 32-bit integer operations
- [i64 Instructions](/instructions/i64) - All 64-bit integer operations
- [f32 Instructions](/instructions/f32) - All 32-bit float operations
- [f64 Instructions](/instructions/f64) - All 64-bit float operations
- [Local & Global](/instructions/local-global) - `local.get`, `local.set`, `local.tee`, `global.get`, `global.set`
- [Control Flow](/instructions/control) - `block`, `loop`, `if`, `br`, `br_if`, `call`, etc.

## Practice

Try small exercises (arithmetic, comparisons, control flow) in [watlings](https://github.com/EmNudge/watlings) to get the stack mental model into your fingers.
