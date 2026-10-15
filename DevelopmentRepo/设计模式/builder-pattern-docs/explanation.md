# About the Builder Pattern

The Builder pattern answers a question Java makes unusually awkward: how do
you construct an object with several optional parts and keep the call site
readable while you do it? This piece gathers the reasoning behind the
pattern, the alternatives it competes with, and the situations where it is
not worth the code it costs.

## The problem builders replace

Consider a user profile with five or six settings, most of them optional.
Java offers several ways to express that, and each grows uncomfortable as
the number of settings rises.

**Telescoping constructors.** One overload for every combination of
optional arguments. The reader must count positions to discover which
argument is the email and which is the username, two parameters of the same
type can be transposed without a word of complaint from the compiler, and
each newly optional field multiplies the number of overloads the class must
carry.

**Constructor arguments that mean "unset".** Passing `null`, `""` or `-1`
as a sentinel. The intent evaporates at the call site, and a legitimate
value can collide with the sentinel, leaving the reader to guess which of
the two was meant.

**Setters after construction.** This works, but it changes what the object
is. The product passes through a state where it exists but is not yet
valid, anyone can call the setters at any later time, the fields cannot be
`final`, and nothing tells a caller how many setters a correct
construction actually requires.

Java has no named arguments - a Kotlin or Swift caller can write
`UserProfile(name = "alice", premium = true)` and be done - so the escape
hatch other languages offer is closed. The builder is what Java developers
reached for instead.

## Why the builder succeeds

A builder resolves these tensions by moving configuration into a separate,
short-lived object. The chain of calls reads like a list of choices rather
than a sequence of positional slots, so adding an optional field adds one
method instead of a family of constructors. Optional fields simply keep
their defaults, which removes the temptation to invent sentinels for them.

Just as importantly, the builder marks a moment. Everything happens between
`new UserProfile.Builder()` and `build()`: configuration is visible,
finished, and checkable in one place. When the required field is missing,
the failure can be raised at `build()` with the name of the field, instead
of surfacing later as a `null` dereference three classes away. Some would
say this single property justifies the pattern on its own, quite apart from
readability.

There is a modest cost, and it should be named: the class grows an extra
inner class, every field is written twice, and a caller who merely wants to
set three values must learn an entry point and a `build()`. The pattern
trades a little machinery for a lot of clarity at the call site - whether
that trade is worthwhile depends on how many callers pay it.

## Builders and immutability

Immutability and optional configuration pull in opposite directions. An
immutable object must be complete at the moment it exists, yet optional
fields mean the caller will not supply everything up front. Setters resolve
the conflict by giving up immutability; builders resolve it by deferring
creation until the last possible moment.

The builder is, in effect, a mutable staging area for an immutable object.
It tolerates half-finished state because it is never handed to anyone but
its own caller, and it collapses into a complete product exactly once.
Java 16 records sharpen this story: a record has a single canonical
constructor and no setters, so a builder pairs naturally with it as the
front door for anything beyond the simplest record.

## The original pattern and the Java idiom

The two are easily confused because they share a name.

The Gang of Four's Builder (1994) separates a construction *process* from
its *representation*. A director marches through the same steps -
"add the header, add the body, add the footer" - while different concrete
builders assemble those steps into HTML, plain text or a binary document.
Its interest is in producing different representations of one construction
sequence, and in controlling the order of the steps.

The Java idiom, popularised by Joshua Bloch in *Effective Java*, drops the
director and the step interface. What remains is a nested class whose
fluent setters collect optional arguments and whose `build()` produces the
product. Its interest is optional arguments, defaults and validation - not
representation.

Both are legitimately called Builder, but the Java idiom is closer to a
convention than to the GoF pattern in full. Understanding which of the two
a colleague means will save a meeting.

## When a builder is overkill

A builder earns its place when a class has many optional parameters, when
several parameters share a type, or when construction must be validated.
When a class has two fields, both required, a plain constructor is shorter
to write, shorter to read, and carries no indirection at all.

Some teams adopt builders as blanket style so that every class looks the
same. The consistency is tempting, and for a codebase that values
uniformity it may be the right call - but it does mean every two-argument
value object in the system pays a tax it does not need. A reasonable rule
of thumb: reach for the builder when the number of optional or
same-typed arguments makes a constructor call ambiguous to read.

## Connections

- **Fluent interfaces** - the Java idiom's chaining is one application of the broader fluent-interface idea; builders are its best-known case.
- **Argument object** - grouping related parameters into a value object solves a related problem; where the argument object is itself configured step by step, the two patterns meet.
- **Factory method** - a static factory decides the type in one call; a builder spreads the same decision across a chain. They are complements more than rivals: `UserProfile.builder()` is itself a factory for the builder.
- **Immutability** - the builder is one of the two standard ways (with the constructor) to create immutable objects that need more arguments than a constructor handles gracefully.

## History

The pattern was codified in *Design Patterns: Elements of Reusable
Object-Oriented Software* (Gamma, Helm, Johnson, Vlissides, 1994), in its
director-driven form. *Effective Java* (Bloch, 1st edition 2001) gave the
Java idiom its canonical shape, and later editions refined it alongside the
rise of immutability as a default preference. Today the idiom appears both
hand-written and generated - Lombok's `@Builder` and the Immutables
library produce exactly the structure this documentation set teaches by
hand.

## Where next

- To implement the idiom from scratch, work through [Your First Builder](tutorial.md).
- For everyday applications, see the [how-to guides](how-to.md).
- For participants, contracts and variants, consult the [reference](reference.md).
