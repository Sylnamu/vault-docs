# How to construct objects with the Builder pattern

This guide shows you how to apply the Builder pattern to common Java
construction problems. Each section is a job in its own right: start with the
one that matches yours. Exact signatures, contracts and variants are in the
[Builder Pattern Reference](reference.md).

## How to replace a telescoping constructor

If a class has grown a chain of constructor overloads - `Widget(String)`,
`Widget(String, String)`, `Widget(String, String, int)` and so on - replace
them with a builder:

1. Create a nested `Builder` class holding one field per constructor parameter.
2. Make the class constructor `private`, take the builder as its only argument, and copy each field across.
3. Add a `public static Builder builder()` method to the class.
4. Rewrite each call site as a chained `build()` call.
5. Delete an overload once a project-wide search shows nothing constructs the object the old way any more.

If two overloads differ only in the order of parameters of the same type,
the compiler will not warn you about swapped arguments. Treat those call
sites as the first ones to migrate, and cover them with a test.

## How to validate input at build time

Keep construction checks in one place, at the end of the chain:

- If `build()` would produce an object missing a required field, throw `IllegalStateException` from `build()`, before the constructor runs.
- If a setter receives a value outside its allowed range - a negative age, an empty name - throw `IllegalArgumentException` from that setter, so the failure names the value that caused it.
- If two fields only make sense in combination, check the combination in `build()`; individual setters cannot see the whole configuration.

The check always runs before the object exists, so callers never receive a
half-valid product to inspect.

## How to keep the constructed object immutable

- Declare every field of the product `final` and assign it from the builder in the constructor.
- If a field holds a `List`, `Map` or array, copy it in the constructor - `List.copyOf(builder.tags)` on Java 10 and later, `new ArrayList<>(builder.tags)` before that - so later changes to the builder cannot reach the built object.
- If callers hand you a collection they might modify afterwards, copy it again inside the builder's setter.
- Give the product no setters; a different configuration means a different builder run.

## How to reuse a builder safely

A builder is a mutable box of unfinished configuration.

- To create several different objects, keep chaining on the same builder and call `build()` whenever you need one; each call produces a new, independent product from the values held at that moment.
- If one builder must be used from more than one thread, either give each thread its own builder or synchronise access to the shared one.
- If a builder is stored in a field for later use, remember that its current values are a half-finished configuration, not a product.

## How to add a field to an existing builder

1. Add the new field to the product as `final`.
2. Copy it from the builder in the constructor. The compiler stops you here if you forget: a `final` field left unassigned is an error.
3. Add the field to the builder, with its fluent setter.
4. Compile before touching call sites; existing chained calls remain valid, because nothing they use has been removed.
5. If the new field is required, add its check to `build()` alongside the existing ones.
