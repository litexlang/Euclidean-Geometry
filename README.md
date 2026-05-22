# Litex Fits Axiomatic Geometry

Hilbert-style geometry is a good test for whether a formal language
can preserve mathematical structure instead of forcing everything
into a low-level encoding first. In this repository, Litex works well
because it lets us write primitive objects, primitive relations, and
axioms in nearly the same shape that they appear in a geometry text.

The point is not that Litex magically solves geometry for us. The
point is that it lets us formalize geometry while keeping the writing
close to the mathematical presentation: points, lines, planes,
incidence, betweenness, congruence, parallelism, and existence-and-
uniqueness constructions can all be stated directly and read back as
mathematics.

- Primitive notions stay primitive. Geometry begins with undefined
terms such as point, line, and plane, together with primitive
relations such as betweenness and congruence. Litex supports this
style naturally: primitive objects can be introduced directly, and
primitive geometric relations can be declared without forcing an
artificial prior definition.
- Axioms look like axioms. Statements such as “for every two distinct
points there exists a unique line through them” or “if two points
of a line lie in a plane, then the whole line lies in that plane”
can be written in Litex in a form that stays very close to the
textbook version. The formalization keeps the familiar shape of
“for every”, “there exists”, “there exists uniquely”, and “if ...
then ...”.
- Standard geometric constructions become standard notation. Once
existence and uniqueness are stated, Litex can introduce the
corresponding object as a function, so familiar expressions such as
line_of(A, B) and plane_of(A, B, C) become available immediately.
This makes the formal development read like ordinary axiomatic
geometry instead of a workaround around the proof language.
- Set-theoretic geometry reads directly. In Hilbert-style geometry,
it is natural to treat lines and planes as collections of points.
Litex already has a readable set-theoretic surface, so membership
statements such as “A lies on l” or inclusion-style statements such
as “the line lies in the plane” can be expressed without extra
encoding overhead.
- Proof development stays local and incremental. After an axiom or
derived fact is stated, it becomes reusable context for later
steps. This is especially useful in geometry, where later arguments
repeatedly depend on small local facts about collinearity,
coplanarity, betweenness, and congruence. Litex supports that style
well because the proof grows fact by fact rather than through large
tactic scripts.

More broadly, this is why Litex is a good fit for repositories like
this one: it allows axiomatic mathematics to remain readable while
still being checkable. For geometry in particular, that matters a
lot, because the value of the subject is not only in what is proved,
but also in how clearly the primitive structure and the logical
dependencies are exposed.