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
We avoid language-level abstractions without performant implementations.

III. Code Expresses Execution
-----------------------------

We avoid features requiring knowledge of the language implementation.
We avoid coercions, implicit function calls, and invisible dispatch.
Translations should predictably impact performance.

IV. Libraries Inhabit A Level Playing Field
-------------------------------------------

No library will be privileged by inclusion within the language itself.
Libraries inhabit a uniform global namespace.
Library distribution is outside the scope of the language implementation.

---
*For an explication of these tenets, see [Lark Memo #2](https://github.com/mptz/lark-memos/blob/master/memos/memo-2.md).*
