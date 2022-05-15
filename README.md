# Programming Language Comparison Cheat Sheet

Pros and cons of widely used programming languages.

- [Performance](#performance)
- [Safety](#safety)
- [Type system](#type-system)
- [Polymorphism](#polymorphism)
- [Pointer](#pointer)
- [Memory safety](#memory-safety)
- [Tooling](#tooling)
- [References](#references)

## Performance

Language | Compiled/interpreted | Process virtual machine (VM) | Garbage collector (GC) | Build time
-- | -- | -- | -- | --
Javascript | JIT | Yes (web browser, node.js) | Yes | -
Typescript | JIT | Yes (web browser, node.js) | Yes | -
Dart | JIT/AOT | Yes (web) / No (mobile) | Yes | -
Python | interpreted | Yes | Yes ([reference counting](https://en.wikipedia.org/wiki/Reference_counting)) | -
Java | JIT | Yes ([JVM](https://en.wikipedia.org/wiki/Java_virtual_machine)) | Yes ([tracing](https://en.wikipedia.org/wiki/Tracing_garbage_collection)) | faster
Go | AOT | No | Yes | faster
Rust | AOT | No | No | slower
C++ | AOT | No | No | slower
C | AOT | No | No | slower

## Safety

Language | Memory safety | Type safety | Null safety | Data race safety
-- | -- | -- | -- | --
Javascript | Yes (GC) | weak | No | No
Typescript | Yes (GC) | strong | Yes | No
Dart | Yes (GC) | strong | Yes | No
Python | Yes (GC) | strong | No | No
Java | Yes (GC) | strong | No | No
Go | Yes (GC) | strong | No | Yes
Rust | Yes ([RAII](https://en.wikipedia.org/wiki/Resource_acquisition_is_initialization)+[ownership](https://doc.rust-lang.org/book/ch04-01-what-is-ownership.html)) | strong | Yes | Yes
C++ | Partially ([RAII](https://en.wikipedia.org/wiki/Resource_acquisition_is_initialization)) | weak | No | No
C | No | weak | No | No

## Type system

Language | Nominal/Structural | Static/Dynamic | Manifest/Inferred | Sum types
-- | -- | -- | -- | --
Javascript | - | dynamic | inferred | No
Typescript | structural | static | manifest | No
Dart | nominal | static | gradual | No
Python | nominal | dynamic | inferred / optional manifest | No
Java | nominal | static | manifest | No
Go | structural | static | partially inferred | No
Rust | mostly nominal | static | manifest / optional inferred | Yes ([enum](https://doc.rust-lang.org/std/keyword.enum.html))
C++ | nominal | static | manifest / optional inferred | No
C | nominal | static | manifest | No

## Polymorphism

Four types of poylmorphism:

1. Ad hoc polymorphism (*overloading*)
2. Parametric polymorphism (*compile-time polymorphism*)
3. Subtype polymorphism (*runtime polymorphism*)
    1. Nominal subtyping (*interface inheritance*)
    1. Structural subtyping (*duck typing*)
4. Coercion polymorphism (implicit or explicit *casting*)

Language | Ad hoc | Parametric | Subtype | Coercion
-- | -- | -- | -- | --
Javascript | No | No | Yes (duck typing) | Yes
Typescript | Yes | Yes | Yes | Yes
Dart | No | Yes | Yes | Yes
Python | No | Yes | Yes (duck typing) | Yes
Java | Yes (overloading) | Yes | Yes | Yes
Go | No | Yes | Yes | Yes
Rust | Yes ([traits](https://doc.rust-lang.org/book/ch10-02-traits.html)) | Yes ([bounded](https://doc.rust-lang.org/book/ch17-01-what-is-oo.html#polymorphism), [generics](https://doc.rust-lang.org/book/ch10-01-syntax.html)) | Yes ([trait objects](https://doc.rust-lang.org/stable/book/ch17-02-trait-objects.html)) | Yes ([type coercions](https://doc.rust-lang.org/reference/type-coercions.html))
C++ | Yes (overloading) | Yes ([templates](https://isocpp.org/wiki/faq/templates)) | Yes | Yes
C | No | No | No | Yes

## Pointer

Language  | Raw pointer | Smart pointer | References
-- | -- | -- | --
Rust | Partially ([unsafe Rust](https://doc.rust-lang.org/book/ch19-01-unsafe-rust.html#unsafe-rust)) | Yes (`std::boxed::Box`, `std::rc::Rc`, `std::sync::Arc`) | Yes
C++ | Yes | Yes (`std::unique_ptr`, `std::shared_ptr`) | Yes
C | Yes| No | No

## Memory safety

Language | Double free | Use after free (dangling pointer) | Null dereferencing
-- | -- | -- | --
Java | No (GC) | No (GC) | Yes (`NullPointerException`)
Go | No (GC) | No (GC) | Yes (`nil pointer dereference`)
Rust | No (ownership rules) | No (borrowing rules) | No (`std::option::Option`)
C++ | Yes | Yes | Yes
C | Yes | Yes | Yes

[Ownership rules](https://doc.rust-lang.org/book/ch04-01-what-is-ownership.html#ownership-rules):

- each value in Rust has a variable that’s called its owner
- there can only be one owner at a time
- when the owner goes out of scope, the value will be dropped

[Borrowing rules](https://doc.rust-lang.org/book/ch04-02-references-and-borrowing.html#the-rules-of-references):

- at any given time, you can have either one mutable reference or any number of immutable references
- references must always be valid

## Tooling

Language | Package manager | Toolchain management | Formatter | Linting | Testing
-- | -- | -- | -- | -- | --
Javascript | `npm` | `nvm` | various | `eslint` | `jest`, `mocha`
Typescript | `npm` | `nvm` | various | `eslint` | `jest`, `mocha`
Python | `pip`, `venv`, `setuptools` | `pyenv` | `autopep8` | `mypy`, `pyright` | `pytest`
Java | `maven`, `gradle` | -- | various | `spotbugs` | `JUnit`, `mockito`
Go | `go` | `go` | `go fmt` | `go vet` | `go test`, `testify`
Rust | `cargo` | `rustup` | `cargo fmt` | `cargo clippy` | `cargo test`
C++ | `vcpkg`, `conan` | -- | -- | -- | --

## References

- Wikipedia, [Comparison of programming languages](https://en.wikipedia.org/wiki/Comparison_of_programming_languages)
- Wikipedia, [Comparison of programming languages by type system](https://en.wikipedia.org/wiki/Comparison_of_programming_languages_by_type_system)
- Peteris Krumins, [The Four Polymorphisms in C++](https://catonmat.net/cpp-polymorphism)
- Steve Klabnik and Carol Nichols, [The Rust Programming Language](https://doc.rust-lang.org/book/)
