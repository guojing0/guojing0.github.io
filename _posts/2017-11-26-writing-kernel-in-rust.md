---
layout: modern
title: The Case for Writing a Kernel in Rust
---

Author: Amit Levy, Bradford Campbell, Branden Ghena, Pat Pannuto, Prabal Dutta, and Philip Levis
Year: 2017

## Summary

Many attempts to add safety mechanisms to kernels have failed, especially these sacrificing performance. But isolation techniques in modern programming languages may help build a safe kernel without sacrificing performance.

With Rust we could avoid runtime memory management and only a small set of unsafe abstractions is needed to form kernel building blocks.

Traditionally people rely on hardware and process abstraction to provide isolation, but the process is heavy-weight. Switching between virtual address space is also costly, but using address spaces for isolation could reduce overhead significantly.

The authors suggest to write the kernel in Rust, a memory-safe programming language, and to entirely throw away hardware protection within the kernel. Since Rust is not garbage collected, it would not complicate memory placement and layout, nor create timing non-determinism that would underline the system.

The primary goal for kernels is to *minimize the amount of unsafe code that must be trusted*. Trusted code is small, including standard abstractions of context switches, call traps, interrupt handling, and memory-mapped I/O, and **TakeCell**, allowing kernel code to safely modify complex data structures *with inline closures that statically compile without overhead*.

### Challenge

The challenge with Rust to write the kernel is that Rust *ownership* only allows one mutable reference, while a kernel needs many.

### Solution

There are two types of unsafe code: one is written by Rust language team, and another is written by kernel developers, but they both provide safe interface.

We could use **Cell** provided by Rust, but it requires copying data out in order to access it, instead of accessing it in place, whose cost could be expensive. Therefore **TakeCell** is provided that does *not* require memory copies.

A kernel usually relies on four Rust abstractions that use unsafe code:

1. Bound checks
2. Iterator optimizations
3. Compiler intrinsics and primitive casts
4. Cell

Six kinds of unsafe kernel code need to be trusted:

1. Context switches
2. Memory-mapped I/O and structures
3. Memory allocator
4. Userspace buffers
5. Interrupt/Exception handlers
6. TakeCell

### Future works

The work by the authors focuses on low-power uniprocessor applications, so future work could be extended to multi-processor kernels, for example, avoiding growing the trusted computing base in service of concurrency.
