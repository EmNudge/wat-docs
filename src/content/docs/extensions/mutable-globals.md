---
title: "Import/Export of Mutable Globals"
description: "Share and modify mutable globals between JS and Wasm."
---


## Export a mutable global from Wasm

```wat
(module
  (global (export "counter") (mut i32) (i32.const 0))
)
```

```javascript
const { instance } = await WebAssembly.instantiate(wasmBytes);
console.log(instance.exports.counter.value); // 0
instance.exports.counter.value = 5;
console.log(instance.exports.counter.value); // 5
```

## Import a mutable global from JS

```wat
(module
  (import "env" "g" (global $g (mut i32)))
  (func (export "inc")
    global.get $g
    i32.const 1
    i32.add
    global.set $g)
)
```

```javascript
const g = new WebAssembly.Global({ value: 'i32', mutable: true }, 0);
const { instance } = await WebAssembly.instantiate(wasmBytes, { env: { g }});
instance.exports.inc();
console.log(g.value); // 1
```

References:

- [Local & Global Instructions](/instructions/local-global) - `global.get`, `global.set`
- [Module Structure](/instructions/module) - `global`, `import`, `export`
- Spec: https://webassembly.github.io/spec/core/syntax/index.html
- Practice: globals in https://github.com/EmNudge/watlings


