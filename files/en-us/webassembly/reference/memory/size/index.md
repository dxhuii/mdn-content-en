---
title: "size: Wasm text instruction"
short-title: size
slug: WebAssembly/Reference/Memory/Size
page-type: webassembly-instruction
browser-compat:
  - webassembly.api.Memory
  - webassembly.multiMemory
spec-urls: https://webassembly.github.io/spec/core/syntax/instructions.html#syntax-instr-memory
sidebar: webassemblysidebar
---

The **`size`** [memory instruction](/en-US/docs/WebAssembly/Reference/Memory) is used to get the current number of pages in a memory.

The instruction adds the size (in pages) to the top of the stack.
Currently each page is 64KiB.

{{InteractiveExample("Wat Demo: size", "tabbed-standard")}}

```wat interactive-example
(module
  (import "console" "log" (func $log (param i32)))
  (memory 2)
  (func $main

    memory.size ;; get the memory size
    call $log ;; log the result

  )
  (start $main)
)
```

```js interactive-example
const url = "{%wasm-url%}";
await WebAssembly.instantiateStreaming(fetch(url), { console });
```

## Syntax

Get size of default memory

```wat
;; Get the number of pages in the default memory
memory.size
;; The number of pages is now added at top of stack
```

Get size of specified memory (if multi-memory supported)

```wat
;; Size of memory with index 1
memory.size (memory 1)

;; Size of memory named $memory2
memory.size (memory $memory2)
```

### Instructions and opcodes

| Instruction   | Binary opcode |
| ------------- | ------------- |
| `memory.size` | `0x3f`        |

## Examples

### Getting size of the default memory

The first memory added to a Wasm module is the default memory and has index 0.
We can get the number of pages in this memory by calling `memory.size`.

The code below shows a WAT file that demonstrates this:

```wat
(module
  (import "console" "log" (func $log (param i32)))
  (memory 1 2) ;; default memory with one page and max of 2 pages

  (func $main
    ;; get size
    memory.size
    call $log ;; log the result (1)

    ;; grow default memory by 1 page
    i32.const 1
    memory.grow

    ;;get size again
    memory.size
    call $log ;; log the result (2)
  )
  (start $main) ;; call immediately on loading
)
```

Above we didn't need to specify the memory index in the `memory.size` instruction, but we could have done so using the memory index (0) of the default memory:

```wat
memory.size (memory 0)
```

For completeness, we can use the compiled version of the above file `size.wasm` with code similar to that shown below (the log function is imported into the module, and called by the module):

```js
start();
async function start() {
  const importObject = {
    console: {
      log(arg) {
        console.log(arg);
      },
    },
  };
  const result = await WebAssembly.instantiateStreaming(
    fetch("size.wasm"),
    importObject,
  );
}
start();
```

### Getting size of a particular memory

As memories are defined in a Wasm module they are sequentially allocated an index number from zero.
You can get the size of a specific memory by specifying the `memory` instruction and the desired index or name (if it has one), after the `memory.size` instruction.
If you don't specify a particular memory the default memory with index 0 is used.

The module below shows how you might directly reference a memory by index and by name.

```wat
(module
  (import "console" "log" (func $log (param i32)))
  (memory 1 2)  ;; Default memory with one page and max of 2 pages
  (memory $memory1 2 4)  ;; Memory with index 1, initial 2 page, max 4 pages
  (func $main
    ;; Get size for memory by index
    memory.size (memory 1)
    call $log ;; log the result (2)

    ;; Get size for memory by memory name
    memory.size (memory $memory1)
    call $log ;; log the result (2)
  )
  (start $main)
)
```

The WAT files could be loaded using the same JavaScript code as the first example.

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

> [!NOTE]
> The `multiMemory` compatibility table indicates versions in which `size` can be used with a specified memory.
