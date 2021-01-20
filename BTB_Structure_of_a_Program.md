#### Back to Basics: The Structure of a Program - Bob Steagall - CppCon 2020

[YouTube Link](https://www.youtube.com/watch?v=3KoXeegncrs)

---
##### Building and running a C++ Program

Input files:

* Header files (.h, .hpp, .hh)
* Source files (.c, .cpp, .cxx)
* Resource files (.res, .qrc, .rcc)

Dependencies (libraries):

* Header files (<vector>)
* Precompiled files (libstdc++.a, libc++.so..)
* Source files (Boost, Catch2)
* Resources (icons, images, translations for I18N)

Compilation: generates one object file for each source file

* Lexical analysis (Tokenization)
* Syntax analysis (Parsing -> Parse tree)
* Semantic analysis ( -> Symbol table)
* Code generation (Turns into machine code)

Linking: the process of combining object files and binary libraries to make a working program

The standard calls the compilation process `translation`

In C++, translation is performed upon a `translation unit (TU)` in nine well defined stated
* Lexical - Phase 1-6
* Syntax, semantic, code gen - Phase 7-8
* Linking - Phase 9

A `translation unit` is defined as
* A source file
* plus all headers and source files included via the `#include` directive
* minus any source lines skipped by conditional inclusion preprocessing directives (`#ifdef`)
* plus all macros expanded

---
##### The One-Definition Rule (ODR)
Guidelines:
* For an `inline` thing (variable of function) that gets used, make sure to define it in at least once in some translation unit
* For everything else that gets used, make it gets define exactly once in one translation unit

---
##### Storage duration and objects
`automatic` storage duration
* object storage is allocated at the beginning of the enclosing block and deallocated at the end of the block
* applies to all local objects except those declared `thread_local`, `static` or `extern`

`dynamic` storage duration
* object storage is allocated and deallocated by the program using functions that perform dynamic memory allocation
* objects with this duration can be create using `new`-expressions and destroyed using `delete`-expressions

`static` storage duration
* object storage is allocated at the beginning of the program and deallocated at the end of the program
* applies to all objects declared at namespace score, including the global namespace
* applies to all objects declared `static` or `extern`
* there is only one instance of an object with static duration in the program

`thread` storage duration
* allocated when the thread creating the object begins and deallocated when that thread ends
* applies only to objects declared `thread_local`
* every thread has its own instance of an object with thread duration

---
##### ABI
ABI (application binary interface) is the platform-specific specification of how entities defined in one TU interacts with entities defined in another TU

GCC and Clang use the Itanium ABI; MSVC uses its own ABI
