Lark Memo #2: Tenet Explication
===============================

This memo explicates the terse and--I hope--pithy
[Lark Language Tenets](https://github.com/mptz/lark-memos/blob/master/memos/memo-1.md).
I try here to provide color, background information, and some degree of
justification for the tenets.  There are many, many ways to design a
programming language, with many conflicting goals; these tenets are not
the "Right Thing", they're simply the ones I've chosen.

I. Lark Targets Rigorous Programming
------------------------------------

> _Lark supports you in writing correct programs.
> Many diverse features support correctness.
> Given the choice between convenience and rigor, we choose rigor._

II. Lark Avoids Overabstraction
-------------------------------

> _Lark runs on real computing hardware with specific capabilities.
> We expose these capabilities to allow high-performance programs.
> We avoid language-level abstractions without performant implementations._

__General Hardware Features__: Lark targets general-purpose programming,
not theorem proving--though theorems can be proven in it.  It supports a
complement of primitive datatypes and operations which correspond to the
native datatypes of general-purpose hardware, or which can be implemented
in low-level code with universally-understood semantics.  Aggregations of
primitive datatypes have similarly low-level implementations, such as
contiguous arrays in main memory.

__Specific Hardware Features__: Lark exposes specific hardware features,
such as the host word size.  We don't try to exhibit identical behavior on
all supported platforms, but we do provide alternatives (such as the *nat*
type for arbitrary-sized natural numbers) which do abstract the language
from its host.  We invest in making these alternatives featureful and
performant, so they can be the default choice.

__Platform Pragmatism__: Lark's datatype semantics reflect a pragmatic
assessment of current and future computing platforms.  We aren't trying
to support general-purpose computing on historical platforms like
16-bit CPUs.  We don't provide for machine word sizes which are not
certain specific powers of 2.  Since the definition of the C language's
more nebulous datatype guarantees, the world of general-purpose hardware
has converged.

## III. Code Expresses Execution

> _We avoid features requiring knowledge of the language implementation.
> We avoid coercions, implicit function calls, and invisible dispatch.
> Translations should predictably impact performance._

## IV. Libraries Inhabit A Level Playing Field

> _No library will be privileged by inclusion within the languge itself.
> Libraries inhabit a uniform global namespace.
> Library distribution is outside the scope of the language implementation._

