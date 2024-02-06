# Introduction to C# - Day 1

## Abbreviations
C# is used to build a variety of applications ranging from web, desktop, to mobile. Some acronyms surrounding C# are:

1. **CLR** - Common Language Runtime (this is the runtime .NET provides; though it supports C#, it also supports other .NET languages).
2. **CTS** - Common Type System (this enables code from multiple languages to interoperate freely, enabling any .NET library to be used by any .NET language, i.e., C# can consume libraries written in F# or Visual Basic).
3. **COM** - Component Object Model (introduced by Microsoft in 1993; it is a binary-interface standard for software components used to enable inter-process communication (IPC) object creation in a large range of programming languages.
4. **IL** - Intermediate Language (this is the language that the C# compiler compiles the code into; it is then executed by the CLR).		
5. **JIT** - Just-In-Time (this is the process of compiling the IL code into machine code at runtime).
6. **AOT** - Ahead-Of-Time (this is the process of compiling the entire application into machine code before it runs).
7. **CLI** - Common Language Infrastructure (this is an open specification developed by Microsoft and standardized by ISO and ECMA that describes executable code and a runtime environment that allows multiple high-level languages to be used on different computer platforms without being rewritten for specific architectures).
8. **VES** - Virtual Execution System (this is the runtime environment that the CLI provides).

## Important Facts about C#

- It is the first programming language designed to be native in the world of the **CLR**.
- The first version of the C# programming language used a model that was closely related to the underlying CLR's model. Even more abstractions have been added in subsequent versions, it was designed to fit well with CLR. This means that in order to understand C#, one needs to understand the CLR and how it runs code.
- C# compiler doesn't work like a traditional compiler. It doesn't compile the code into machine code. Instead, it compiles the code into an **IL** that is then executed by the CLR. This is why C# is called a managed language. The CLR manages the execution of the code. The use of IL enables features that are not available in traditional compilers. For example, the CLR can optimize the IL code for the specific hardware it is running on. This means that the same IL code can run on different hardware without modification.
- The executable binary is produced later (not always) at runtime by the CLR.
- In order to generate executable machine code, the CLR uses a JIT compilation approach, in which each individual function is compiled the first time it runs. But .NET also supports AOT compilation, which compiles the entire application into machine code before it runs. This is useful for mobile and gaming platforms, where JIT compilation can be slow and consume a lot of memory.

## Philosophy Underpinning C#'s Design

> Prefer generality to specialization, because _generality leads to reusability_.

Though C# language designers always have specific scenarios in mind for new features, they try to design them in a way that makes them generally useful. This is why C# has a rich set of features that can be used in a variety of scenarios.

## Unanswered Trivial Questions

1. **What is the acronym of .NET?**
2. **Where did C# got its name from?**
