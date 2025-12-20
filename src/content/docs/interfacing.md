---
title: Interfacing with Hosts
description: Import functions, export APIs, and share memory to call WAT modules from JavaScript and other hosts.
---

Most real programs talk to a host (like JavaScript) via imports/exports and linear memory.

For authoritative syntax and semantics, see the [WebAssembly spec — Structure → Modules, Imports, Exports, Memories](https://webassembly.github.io/spec/core/syntax/index.html).

## Imports and exports

```wat
(module
  ;; Import a function `env.log: (i32) -> ()`
  (import "env" "log" (func $log (param i32)))

  ;; Export a function and a memory
  (memory $mem 1)                      ;; 1 page = 64 KiB
  (export "memory" (memory $mem))

  (func $add (param $a i32) (param $b i32) (result i32)
    local.get $a
    local.get $b
    i32.add)
  (export "add" (func $add))
)
```

- Imports bring host functionality into the module, namespaced by module string (e.g., `"env"`).
- Exports make module items available to the host by name.

## Calling from JavaScript

```javascript
// Assume you have compiled WAT to .wasm bytes (e.g., with wasm-tools or wat2wasm).
const wasmBytes = await fetch('/path/to/module.wasm').then(r => r.arrayBuffer());

const imports = {
  env: {
    log: (x) => console.log('WASM says:', x),
  },
};

const { instance } = await WebAssembly.instantiate(wasmBytes, imports);
console.log(instance.exports.add(20, 22)); // 42
```

- JS import object shape matches your `(import "module" "name" ...)` declarations.
- Exported functions are regular callable JS functions. Memories and tables are objects.

## Working with linear memory

You can share bytes via a `memory` export. From JS, view it as a typed array.

```wat
(module
  (memory $mem 1)
  (export "memory" (memory $mem))

  ;; Write a byte at an offset
  (func $write_byte (param $offset i32) (param $value i32)
    local.get $value
    local.get $offset
    i32.store8)                 ;; store 8-bit at memory[offset]
  (export "write_byte" (func $write_byte))
)
```

```javascript
const { instance } = await WebAssembly.instantiate(wasmBytes);
const mem = new Uint8Array(instance.exports.memory.buffer);

instance.exports.write_byte(0, 0x48);     // 'H'
instance.exports.write_byte(1, 0x69);     // 'i'
console.log(new TextDecoder().decode(mem.subarray(0, 2))); // "Hi"
```

Notes:

- Memory is grown in 64 KiB pages; you can allow growth with `(memory min max?)`. If you grow, the underlying `ArrayBuffer` can change; refresh your typed array views after growth.
- Loads/stores are typed instructions: `i32.store`, `i32.store8`, `i32.load`, etc. Alignment hints are optional in text format.

## Passing strings

Wasm deals in bytes, so strings are a convention: encode to bytes on the host, pass a pointer/length to Wasm, and decode on the other side. A simple pattern from JS:

```javascript
function writeString(memU8, offset, str) {
  const bytes = new TextEncoder().encode(str);
  memU8.set(bytes, offset);
  return bytes.length;
}
```

On the Wasm side, consume bytes starting at the offset for the given length.

## Tables and function references

To call back and forth with function references:

```wat
(module
  (table 1 funcref)
  (type $t0 (func (param i32) (result i32)))
  (func $inc (type $t0) (param $x i32) (result i32)
    local.get $x
    i32.const 1
    i32.add)
  (elem (i32.const 0) $inc)
  (func (export "call0") (param $n i32) (result i32)
    i32.const 0
    call_indirect (type $t0)      ;; call function at table index 0
    )
)
```

From JS, you can also supply host funcs via imports and store them in tables if desired.

## Tooling note

This site assumes you’re working in WAT. For learn-by-doing exercises and a `wasm-tools`-based workflow, try [watlings](https://github.com/EmNudge/watlings). Its scripts rely on `wasm-tools parse` to assemble WAT to Wasm.


