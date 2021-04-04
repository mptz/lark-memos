Lark Memo #2: Tenet Explication
===============================

This memo explicates the terse and--I hope--useful and pithy
[Lark Language Tenets](https://github.com/mptz/lark-memos/blob/master/memos/memo-1.md).
I try here to provide color, background information, and some degree of
justification for the tenets.  There are many, many ways to design a
programming language, with many conflicting goals; these tenets are not
the "Right Thing", they simply reflect design choices I've made.  I should
say made *for now*, since I'm grateful to be guided onto a better path.

I. Lark Targets Rigorous Programming
------------------------------------

> _Lark supports you in writing correct programs.
> Many diverse features support correctness.
> Given the choice between convenience and rigor, we choose rigor._

II. Lark Avoids Overabstraction
-------------------------------

> _Lark runs on real computing hardware with specific capabilities.
> We expose these capabilities to allow high-performance programs.
> Abstractions should coincide with performant implementations.
> High degrees-of-freedom abstraction designs are delegated to libraries._

__General Hardware Features__: Lark targets general-purpose programming,
not theorem proving--though theorems can be proven in it.  It supports a
complement of primitive datatypes and operations which correspond to the
native datatypes of general-purpose hardware, or which can be implemented
in low-level code with universally-understood semantics.  Aggregations of
primitive datatypes have similarly low-level implementations, such as
contiguous arrays in main memory.

__Specific Hardware Features__: Lark exposes specific hardware features,
such as the host word size.  We don't try to exhibit identical behavior on
all supported platforms, but we do provide alternatives (such as the *Nat*
type for arbitrary-sized natural numbers) which can abstract the language
from its host.  We invest in making these alternatives featureful and
performant, so they can be the default choice.

__Platform Pragmatism__: Lark's datatype semantics reflect a pragmatic
assessment of current and future computing platforms.  We aren't trying
to support general-purpose computing on historical platforms like
16-bit CPUs.  We don't provide for machine word sizes which are not
certain specific powers of 2.  Since the definition of the C language's
more nebulous datatype guarantees, the world of general-purpose hardware
has converged.

__Batteries Not Included__: This tenet guides us away from embedding
concepts in the core language once the implementations of those concepts
have many degrees of freedom.  This is best illustrated by examples:

* Complex numbers are included in many languages, and work well in many
  of them.  Fortran, for example, has a scientific-computing focus and an
  emphasis on hardware-supported, fixed-width, floating-point types which
  guides it towards a specific representation of complex numbers.  But in
  a general-purpose language with a variety of native numeric types, how
  do we represent a complex number?  At a high level, we could choose a
  representation based on orthogonal real and imaginary parts, though some
  applications are better served by polar representation with radius and
  phase angle.  But even if we settle on a+bi as our representation, what
  should be the types of a and b?  IEEE floating point would be convenient
  for numeric computing, with many trigonometric functions already
  available--but do you want single-precision for speed and massively
  parallel processing, or double-precision for... well, precision?  And
  will floating point do the job?  When our language's native integral
  types are unbounded, don't we want a complex number representation which
  can also handle arbitrary magnitude?

* Rationals are included in a smaller number of languages, and provide
  built-in support for exact numeric operations.  But if exact computation
  is your priority, you can do better than rationals, which can explode in
  magnitude with specific operations.

* Sets and dictionaries have even more design considerations.  Are they
  implemented using sorting or hashing?  Are objects iterable, and if so
  are they iterable in sorted order?

These examples share some common themes: they are useful abstractions,
they can be implemented on top of lower-level abstractions (for example,
by composing floating-point number into complex numbers or unbounded
integers into rationals), and they all have a number of degrees of freedom
in their implementation spaces; choosing a specific implementation will
inevitably leave some use cases poorly served.

__Lark Is Not A Scripting Language__ (expand on this).

## III. Code Expresses Execution

> _We avoid features requiring knowledge of the language implementation.
> We avoid coercions, implicit function calls, and invisible dispatch.
> We're wary of excessively-terse code and anonymous entities.
> Translations should predictably impact performance._

## IV. Lark Targets Global Scale

> _Namespace allocation is decentralized and robust.
> Change is inevitable, so primitive features support evolution.
> Source code files are abstract.
> Dependencies are extralinguistic._

For example no include or import statements.  This allows flexibility
of approach for managing code artifacts.

## V. Compilation Is Preparation

> _Lark embraces a strong phase distinction.
> Compilation encompasses translation, specialization, and verification.
> Compiled objects can have rich read-only structure.
> Lark executation environments are lightweight and start quickly._

Virtual execution environments should also be reentrant.  Users should
thinking nothing of running a Lark program interactively, a developers
should think nothing of spinning up a Lark VM from a C program.

We encourage small heaps; the quickest way to GC is to exit.  We favor
copying data over big shared heaps.

We care not just about startup time of the runtime itself, but also
about the amount of data structure initialization the application requires.
Common, immutable data structures should reside outside heaps--it should
be possible to serialize/deserialize & compile data structures including
those made up of inductive types and other pointer-bearing structures.

## VI. Libraries Inhabit A Level Playing Field

> _No library will be privileged by inclusion within the languge itself.
> Libraries inhabit a uniform global namespace.
> Library distribution is outside the scope of the language implementation._

