# Sesi Language - Complete Implementation Summary

## 📋 Overview

**Sesi** is a highly legible, buildable **programming language**. It provides clean primitives for executing robust internal logic and external APIs, acting as the ideal layer to parse text, orchestrate shell commands, and interact with the file system. Unlike traditional languages that require sprawling SDKs for even basic interactions, Sesi integrates command execution naturally, enabling developers to build context-aware scripts with minimal boilerplate.

1. **Practical Over Perfect**: Focus on what developers actually need, not theoretical completeness.
2. **Transparency Over Magic**: Sesi runs exactly what you write with clear costs and execution maps.
3. **Simplicity First**: A custom tree-walking interpreter for clarity and maintainability.
4. **Type Safety with Flexibility**: Static types for normal code, runtime checking for integration outputs.


## 🔧 Technology Stack

| Component | Technology               | Rationale                                |
| --------- | ------------------------ | ---------------------------------------- |
| Language  | TypeScript               | Type safety, IDE support, easy debugging |
| Runtime   | Node.js 18+              | Wide availability, async support         |
| Parser    | Recursive descent        | Simple, readable, extensible             |
| Execution | Tree-walking interpreter | Easy to understand and modify            |
| Testing   | Typescript               | Standard Node.js test framework          |

**Why this stack?**

- **Tree-walking interpreter over bytecode**: Easier to understand, modify, and debug. No premature optimization.
- **TypeScript over JavaScript**: Catch errors early, better IDE support, self-documenting code.
- **Recursive descent over other parsers**: Handles the grammar perfectly, easy to add language features.

## 🌟 Language Features (V1)

### Core Language ✅

**Variables & Bindings**

```sesi
let x = 10
let PI = 3.14159
let y  // null initially
```

**Functions**

```sesi
fn add(a: number, b: number) -> number {return a + b}

fn greet(name: string = "World") {print "Hello, " + name}
```

**Control Flow**

```sesi
if condition { ... } else { ... }
while condition { ... }
for x = 0 to 10 { ... }
for item in array { ... }
try { ... } catch (e) { ... }
```

**Operators**

- Arithmetic: `+`, `-`, `*`, `/`, `%`
- Comparison: `==`, `!=`, `<`, `>`, `<=`, `>=`
- Logical: `&&`, `||`, `!`
- Assignment: `=`

**Data Types**

- Primitives: `number`, `string`, `bool`, `null`
- Collections: `array<T>`, `object<T>`
- Functions: First-class values
- Union types: `T | U`
- Optional: `T?`

**Scoping**

- Lexical scoping with environment chain
- Block scope for loops/conditionals
- Closure support

**Prompt Blocks**

```sesi
prompt pageContent {"<body...</div>>}
prompt header {"<header...</div>>}
```

**Structured Output**

```sesi
let rawJson = "{\"projectName\": \"Sesi\", \"version\": \"1.3.0\", \"status\": \"active\"}"
let parsedRegistry = structured_output({projectName: string, version: string, status: string})(rawJson)
```

**Implicit Statement Termination** ✅

Expressions ending in `}` (such as prompt blocks) no longer strictly require a newline or semicolon to terminate, allowing for cleaner one-liner syntax.

**Tool Calling**

```sesi
let result = tool_call(functionName)("myTool", {"arg":"val"})
```

**Memory**

```sesi
try {
    let data = "{\"projectName\": \"Sesi\", \"version\": \"1.3.0\", \"status\": \"active\"}"
    memory storedDB { data }
    print "Current DB:" storedDB
    let new_data = "{\"projectName\": \"Sesi\", \"version\": \"1.3.2\", \"status\": \"active\"}"
    print "New Data:" new_data
    storedDB = storedDB + new_data
    print "Current DB:" storedDB
} catch (e) {
    print "Error:" e
}
```

## 🌍 Built-in Global Variables

- `args` (`array<string>`): Contains the command-line arguments passed to the script, excluding Sesi runtime options and the script path.

## 🛠️ Built-in Functions

### I/O

- `print(...args)` - Output to stdout
- `read_file(path)` - Read file contents
- `write_file(path, content)` - Write file contents
- `write_image(path, content)` - Write base64 image data to file
- `from_json(path)` - Read a JSON file
- `list_dir(path)` - List directory contents
- `make_dir(path)` - Create a new directory
- `spawn(path)` - Launch concurrent background process
- `exec(command)` - Synchronous shell execution
- `time()` - Unix timestamp (ms)
- `random()` - Random number (0-1)

### Type Functions

- `type(value)` - Get type name
- `str(value)` - Convert to string
- `to_json(value)` - Convert to JSON string
- `num(value)` - Convert to number
- `bool(value)` - Convert to boolean

### Collection Functions

- `len(collection)` - Get length
- `push(array, value)` - Add element
- `pop(array)` - Remove element
- `join(array, sep)` - Join to string
- `split(string, sep)` - Split to array
- `keys(object)` - Get keys
- `values(object)` - Get values
- `range(n)` - Create range array

### Network

- `web_get(url, headers)` - Perform HTTP GET request
- `web_send(url, body, headers)` - Perform HTTP POST request

### Concurrency

- `multi_req(fns)` - Concurrently execute multiple closures/functions

## Tool Use

- `define_tool(name, fn, description)` - Register a custom tool
- `list_tools()` - List custom tool names

### Error Handling

- `error_type(type, message, data)` - Create a custom error object
- `raise_error(type_or_error, message, data)` - Throw an error

### Math

- `exp(x)` - Exponential function

## 📊 Implementation Statistics

| Built-in functions  | 34     |
| Supported operators | 20+    |
| AST node types      | 30+    |
| Token types         | 50+    |


## 💡 Key Implementation Details

### Lexer Design

- Character-by-character scanning
- Keyword recognition
- String/number literal parsing
- Comment stripping
- Position tracking for error messages

### Parser Design

- Recursive descent parsing
- Expression precedence (11 levels)
- Error recovery via synchronization
- Full AST construction
- Support for all language constructs

### Interpreter Design

- Tree-walking evaluation
- Environment chain for scoping
- Async support for reasoning calls
- Control flow exceptions (return, break, continue)
- Built-in function dispatch


Sesi is not just an experiment in language design. Use it to learn, explore, and evolve what the future of coding will become.

Sesi is a highly legible, buildable **programming language**. It provides clean primitives for executing robust internal logic and external APIs, acting as the ideal layer to parse text, orchestrate shell commands, and interact with the file system. Unlike traditional languages that require sprawling SDKs for even basic interactions, Sesi integrates command execution naturally, enabling developers to build context-aware scripts with minimal boilerplate.


