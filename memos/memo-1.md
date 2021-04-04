Lark Memo #1: Lark Tenets
=========================

I. Lark Targets Rigorous Programming
------------------------------------

Lark supports you in writing correct programs.
Many diverse features support correctness.
Given the choice between convenience and rigor, we choose rigor.

II. Lark Avoids Overabstraction
-------------------------------

Lark runs on real computing hardware with specific capabilities.
We expose these capabilities to allow high-performance programs.
Abstractions coincide with performant implementations.
High degrees-of-freedom abstraction designs are delegated to libraries.

III. Code Expresses Execution
-----------------------------

We avoid features requiring knowledge of the language implementation.
We avoid coercions, implicit function calls, and invisible dispatch.
We're wary of excessively-terse code and anonymous entities.
Translations should predictably impact performance.

IV. Lark Targets Global Scale
-----------------------------

Namespace allocation is decentralized and robust.
Change is inevitable, so primitive features support evolution.
Language files are abstract.
Dependencies and configuration are extralinguistic.

V. Compilation Is Preparation
-----------------------------

Lark embraces a strong phase distinction.
Compilation encompasses translation, specialization, and verification.
Compiled objects can have rich read-only structure.
Lark execution environments are lightweight and start quickly.

VI. Libraries Inhabit A Level Playing Field
-------------------------------------------

We limit builtins to the transitive closure of language features.
No library will be privileged by inclusion within the language itself.
Libraries inhabit a uniform global namespace.
Library distribution is outside the scope of the language implementation.

---
*For an explication of these tenets, see [Lark Memo #2](https://github.com/mptz/lark-memos/blob/master/memos/memo-2.md).*
