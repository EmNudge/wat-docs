---
title: 'JS BigInt ↔ Wasm i64'
description: 'Map JavaScript BigInt to WebAssembly i64 parameters and results.'
---

Modern JS engines map Wasm `i64` to JavaScript `BigInt`. You can pass `BigInt` values to Wasm functions that take `i64` and receive `BigInt` from `i64` results.

```wat
(module
  (func (export "inc64") (param $x i64) (result i64)
    local.get $x
    i64.const 1
    i64.add)
)
```

```javascript
const { instance } = await WebAssembly.instantiate(wasmBytes);
// BigInt in, BigInt out:
console.log(instance.exports.inc64(41n)); // 42n
```

Notes:

- Non-BigInt JS numbers are not accepted for `i64` parameters.
- Passing `BigInt` to non-`i64` params will throw.

References:

- [i64 Instructions](/instructions/i64) - Complete reference for all i64 operations
- [Type Names](/instructions/types) - `i64` type reference
- Spec types overview: https://webassembly.github.io/spec/core/syntax/index.html
- Practice: i64 exercises in https://github.com/EmNudge/watlings
