# Builder Pattern Reference

Classification: creational design pattern. Origin: Gang of Four, *Design Patterns* (1994). The descriptions below cover both the original form of the pattern and the fluent Java idiom derived from it.

## Intent

Construct a complex object step by step, separating the construction process from the representation of the result.

## Participants

| Participant | Responsibility |
|-------------|----------------|
| Builder | Declares the operations for building parts of a product. |
| Concrete Builder | Implements the builder operations; provides and assembles the parts of a concrete product. |
| Director | Optional. Constructs a product by calling the builder's operations in a fixed order. |
| Product | The complex object being constructed. |
| Client | Selects a concrete builder, drives construction (directly or through the director), and receives the product. |

## Structure: director-driven form

```java
interface Builder {
    void buildPartA();
    void buildPartB();
    Product getResult();
}

class Director {
    void construct(Builder builder) {
        builder.buildPartA();
        builder.buildPartB();
    }
}
```

## Structure: fluent Java idiom

```java
class Widget {

    private final String name;
    private final int size;

    private Widget(Builder builder) {
        this.name = builder.name;
        this.size = builder.size;
    }

    static Builder builder() {
        return new Builder();
    }

    static final class Builder {
        private String name;
        private int size;

        Builder name(String name) {
            this.name = name;
            return this;
        }

        Builder size(int size) {
            this.size = size;
            return this;
        }

        Widget build() {
            return new Widget(this);
        }
    }
}
```

## Contracts

The contracts below describe the fluent Java idiom shown above.

- `builder()` returns a new builder whose fields hold their default values.
- Each setter stores its argument and returns the same builder instance.
- `build()` returns a fully initialised product.
- `build()` throws `IllegalStateException` if a required field is unset (documented idiom; the exception type is set by each class).
- A builder is mutable and not thread-safe.
- Default field values: `null` for reference types, `0` for `int`, `false` for `boolean`.
- Each `build()` call creates a new product; the builder retains its stored values after the call.

## Variants

| Variant | Distinguishing feature |
|---------|------------------------|
| Director-driven builder (GoF) | A director sequences the steps; several concrete builders yield different representations of the same construction process. |
| Incremental-product builder (GoF) | The product is assembled and refined step by step; `getResult()` may be called before construction is complete. |
| Fluent nested-class builder (Java idiom) | Steps chain by returning `this`; no director; the product is created once, in `build()`. |
| Copy-on-write builder | Each setter returns a new builder, leaving the previous one unchanged. |
| Annotation-generated builder (Lombok `@Builder`, Immutables) | The fluent idiom above is generated from fields or accessors. |

## Constraints

These constraints apply to the fluent Java idiom.

- The product constructor is `private` and takes the builder; all construction passes through `build()`.
- The builder is a static nested class, so it is reachable as `OuterClass.Builder` without an instance of the outer class.
- The product's fields are `final` when the product is immutable.
- In the fluent idiom, setters return `this`, not a new builder.
- The product exposes no setters.

## Example

```java
UserProfile user = new UserProfile.Builder()
        .username("alice")
        .email("alice@example.com")
        .age(30)
        .build();
```

## Related patterns

- **Abstract Factory** - creates families of related objects without exposing the sequence of construction steps; a builder exposes the steps and lets the caller order them.
- **Static factory method** - construction in a single call; all parameters are decided at once rather than across a chain.
- **Composite** - the GoF text notes that builders are often used to construct Composite structures.
- **Fluent interface** - the chaining convention used by the Java idiom; the builder is one application of it.
