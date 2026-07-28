# Programming Languages Quick Reference

> Side-by-side syntax for Python, JavaScript/TypeScript, Rust, and Go. Print this or bookmark it.

---

## Variables

| Task | Python | JavaScript | TypeScript | Rust | Go |
|------|--------|------------|------------|------|-----|
| Immutable | `x = 1` | `const x = 1` | `const x = 1` | `let x = 1` | `x := 1` |
| Mutable | `x = 1` | `let x = 1` | `let x = 1` | `let mut x = 1` | `var x int = 1` |
| Type annotation | `x: int = 1` | `const x: number = 1` | `const x: number = 1` | `let x: i32 = 1` | `var x int = 1` |
| Null/None | `None` | `null` | `null` | `None` | `nil` |
| Undefined | — | `undefined` | `undefined` | — | — |

## Functions

| Task | Python | JavaScript | TypeScript | Rust | Go |
|------|--------|------------|------------|------|-----|
| Define | `def f(a, b):` | `function f(a, b) {` | `function f(a: string, b: number): void {` | `fn f(a: i32, b: i32) -> i32 {` | `func f(a int, b int) int {` |
| Arrow/lambda | `f = lambda x: x+1` | `const f = (x) => x+1` | `const f = (x: number) => x+1` | `\|x\| x + 1` | `func(x int) int { return x+1 }` |
| Default args | `def f(x=10):` | `function f(x = 10) {` | `function f(x = 10) {` | — | — |
| Variadic | `def f(*args):` | `function f(...args) {` | `function f(...args: number[]) {` | — | `func f(args ...int) {` |
| Return | `return x` | `return x` | `return x` | `x` (no semicolon) | `return x` |
| Multiple return | `return a, b` | `return [a, b]` | `return [a, b]` | `(a, b)` tuple | `a, b` |

## Data Structures

### Lists / Arrays

| Task | Python | JavaScript | TypeScript | Rust | Go |
|------|--------|------------|------------|------|-----|
| Literal | `[1, 2, 3]` | `[1, 2, 3]` | `[1, 2, 3]` | `vec![1, 2, 3]` | `[]int{1, 2, 3}` |
| Access | `lst[0]` | `arr[0]` | `arr[0]` | `v[0]` | `arr[0]` |
| Length | `len(lst)` | `arr.length` | `arr.length` | `v.len()` | `len(arr)` |
| Push | `lst.append(x)` | `arr.push(x)` | `arr.push(x)` | `v.push(x)` | `append(arr, x)` |
| Slice | `lst[1:3]` | `arr.slice(1, 3)` | `arr.slice(1, 3)` | `&v[1..3]` | `arr[1:3]` |

### Dictionaries / Objects / Maps

| Task | Python | JavaScript | TypeScript | Rust | Go |
|------|--------|------------|------------|------|-----|
| Literal | `{"k": "v"}` | `{"k": "v"}` | `{"k": "v"}` | `HashMap::from([("k","v")])` | `map[string]string{"k":"v"}` |
| Access | `d["k"]` | `obj.k` | `obj.k` | `m.get("k")` | `m["k"]` |
| Set | `d["k"] = v` | `obj.k = v` | `obj.k = v` | `m.insert("k",v)` | `m["k"] = v` |
| Delete | `del d["k"]` | `delete obj.k` | `delete obj.k` | `m.remove("k")` | `delete(m, "k")` |
| Check key | `"k" in d` | `"k" in obj` | `"k" in obj` | `m.contains_key("k")` | `_, ok := m["k"]` |

## Control Flow

| Task | Python | JavaScript | TypeScript | Rust | Go |
|------|--------|------------|------------|------|-----|
| If | `if x:` | `if (x) {` | `if (x) {` | `if x {` | `if x {` |
| Else if | `elif x:` | `else if (x) {` | `else if (x) {` | `} else if x {` | `} else if x {` |
| Else | `else:` | `else {` | `else {` | `} else {` | `} else {` |
| For each | `for x in lst:` | `for (const x of arr) {` | `for (const x of arr) {` | `for x in &v {` | `for _, x := range arr {` |
| For range | `for i in range(n):` | `for (let i=0; i<n; i++) {` | `for (let i=0; i<n; i++) {` | `for i in 0..n {` | `for i := 0; i < n; i++ {` |
| While | `while x:` | `while (x) {` | `while (x) {` | `while x {` | `for x {` |
| Match/Switch | `match x:` | `switch (x) {` | `match (x) {` | `match x {` | `switch x {` |

## Error Handling

| Task | Python | JavaScript | TypeScript | Rust | Go |
|------|--------|------------|------------|------|-----|
| Try | `try:` | `try {` | `try {` | — | — |
| Catch | `except E as e:` | `catch (e) {` | `catch (e) {` | — | — |
| Throw | `raise E("msg")` | `throw new Error("msg")` | `throw new Error("msg")` | `return Err(e)` | `return fmt.Errorf("msg")` |
| Result type | — | — | — | `Result<T, E>` | `val, err := f()` |
| Panic | `raise` (uncaught) | `throw` (uncaught) | `throw` (uncaught) | `panic!("msg")` | `panic("msg")` |

## Classes & Structs

| Task | Python | JavaScript | TypeScript | Rust | Go |
|------|--------|------------|------------|------|-----|
| Define | `class Foo:` | `class Foo {` | `class Foo {` | `struct Foo {` | `type Foo struct {` |
| Constructor | `def __init__(self):` | `constructor() {` | `constructor() {` | `impl Foo { fn new() -> Self {` | `func NewFoo() *Foo {` |
| Method | `def method(self):` | `method() {` | `method() {` | `fn method(&self) {` | `func (f *Foo) Method() {` |
| Inherit | `class Bar(Foo):` | `class Bar extends Foo {` | `class Bar extends Foo {` | `trait` (no inheritance) | Embedding |
| Implement | — | — | — | `impl Trait for Foo {` | — |

## Imports

| Task | Python | JavaScript | TypeScript | Rust | Go |
|------|--------|------------|------------|------|-----|
| Import | `import os` | `import fs from "fs"` | `import fs from "fs"` | `use std::fs;` | `"fmt"` |
| From import | `from os import path` | `import { join } from "path"` | `import { join } from "path"` | `use std::path::Path;` | `"path/filepath"` |
| Alias | `import numpy as np` | `import * as R from "ramda"` | `import * as R from "ramda"` | `use std::collections::HashMap as HM` | — |
| Wildcard | `from os import *` | `import * from "os"` | — | `use std::*;` | — |

## Common Gotchas

| Language | Gotcha | Solution |
|----------|--------|----------|
| Python | Mutable default args | Use `None` + check |
| JS | `===` vs `==` | Always use `===` |
| TS | `any` type creep | Enable `strict` mode |
| Rust | Ownership errors | Clone or use references |
| Go | Ignored errors | Always check `err` |

---

> **Full section:** [Languages](../06-programming-languages/README.md) | **Next:** [Package Managers](package-managers-quick-reference.md)
