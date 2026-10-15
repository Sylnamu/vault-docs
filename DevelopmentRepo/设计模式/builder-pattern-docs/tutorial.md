# Tutorial: Your First Builder

In this tutorial we will build a `UserProfile` class together with its
builder, in a single Java file. By the end you will run the program and see
two user profiles printed in the terminal: one configured with every field,
and one with only the essentials.

## What you need

- A JDK, version 8 or newer (check with `javac -version`)
- A text editor
- A terminal

No libraries and no IDE are required. Everything goes into one file called
`UserProfile.java`.

## Step 1: Create the skeleton

Create `UserProfile.java` with this content:

```java
public class UserProfile {

    private final String username;
    private final String email;
    private final int age;
    private final boolean premium;

    private UserProfile(Builder builder) {
        this.username = builder.username;
        this.email = builder.email;
        this.age = builder.age;
        this.premium = builder.premium;
    }

    public static class Builder {
        private String username;
        private String email;
        private int age;
        private boolean premium;
    }

    public static void main(String[] args) {
        System.out.println("UserProfile is ready");
    }
}
```

Compile and run it now, before changing anything further:

```bash
javac UserProfile.java
java UserProfile
```

You should see:

```
UserProfile is ready
```

Notice that the constructor is `private`, so from this point on only the
builder can create `UserProfile` objects. (Why that matters is discussed in
[About the Builder Pattern](explanation.md); for now, simply follow the
steps.)

## Step 2: Add the fluent setter methods

Add these four methods inside the `Builder` class, below its four fields:

```java
        public Builder username(String username) {
            this.username = username;
            return this;
        }

        public Builder email(String email) {
            this.email = email;
            return this;
        }

        public Builder age(int age) {
            this.age = age;
            return this;
        }

        public Builder premium(boolean premium) {
            this.premium = premium;
            return this;
        }
```

Compile again with `javac UserProfile.java`. You should see no output at
all: `javac` prints nothing when a file compiles cleanly.

Notice that every method returns `this`. That single detail is what will let
the calls chain together in the next step.

## Step 3: Add build() and create the first profile

Add this method inside the `Builder` class, below the four setter methods:

```java
        public UserProfile build() {
            if (username == null) {
                throw new IllegalStateException("username is required");
            }
            return new UserProfile(this);
        }
```

Then replace the `main` method with this one:

```java
    public static void main(String[] args) {
        UserProfile alice = new UserProfile.Builder()
                .username("alice")
                .email("alice@example.com")
                .age(30)
                .premium(true)
                .build();

        System.out.println(alice.username + " is premium: " + alice.premium);
    }
```

Compile and run:

```bash
javac UserProfile.java
java UserProfile
```

You should see:

```
alice is premium: true
```

Notice that the whole configuration reads as one sentence ending at
`build()`, and that the finished object arrives with every field already
assigned.

Now let the safety net show itself. Comment out the line
`.username("alice")`, then compile and run the program again. You will see:

```
Exception in thread "main" java.lang.IllegalStateException: username is required
```

Uncomment the line before continuing.

## Step 4: Build a second profile with fewer fields

Add this block inside `main`, below the first profile:

```java
        UserProfile bob = new UserProfile.Builder()
                .username("bob")
                .email("bob@example.com")
                .age(24)
                .build();

        System.out.println(bob.username + " is premium: " + bob.premium);
```

Compile and run the program once more. The output should now be:

```
alice is premium: true
bob is premium: false
```

Notice that Bob's profile never called `premium(...)`, yet `build()`
succeeded and the field simply kept its default value. Optional fields need
no overloads and no placeholder arguments.

If you would like to practise the feeling of doing, build a third profile
with values of your own and print it too.

## The complete file

Your file should now look like this:

```java
public class UserProfile {

    private final String username;
    private final String email;
    private final int age;
    private final boolean premium;

    private UserProfile(Builder builder) {
        this.username = builder.username;
        this.email = builder.email;
        this.age = builder.age;
        this.premium = builder.premium;
    }

    public static class Builder {
        private String username;
        private String email;
        private int age;
        private boolean premium;

        public Builder username(String username) {
            this.username = username;
            return this;
        }

        public Builder email(String email) {
            this.email = email;
            return this;
        }

        public Builder age(int age) {
            this.age = age;
            return this;
        }

        public Builder premium(boolean premium) {
            this.premium = premium;
            return this;
        }

        public UserProfile build() {
            if (username == null) {
                throw new IllegalStateException("username is required");
            }
            return new UserProfile(this);
        }
    }

    public static void main(String[] args) {
        UserProfile alice = new UserProfile.Builder()
                .username("alice")
                .email("alice@example.com")
                .age(30)
                .premium(true)
                .build();

        System.out.println(alice.username + " is premium: " + alice.premium);

        UserProfile bob = new UserProfile.Builder()
                .username("bob")
                .email("bob@example.com")
                .age(24)
                .build();

        System.out.println(bob.username + " is premium: " + bob.premium);
    }
}
```

## If something goes wrong

- `cannot find symbol: class Builder` - the code from step 2 or 3 landed
  outside the `Builder` class. Check that its closing brace comes after your
  last method.
- `missing return statement` - one of the setter methods is missing its
  `return this;` line.
- `';' expected` - a brace or a semicolon was lost; compare your file with
  the complete listing above.
- `IllegalStateException: username is required` - the `.username(...)` line
  is still commented out from the experiment in step 3.

## Where next

You have built a working builder and used it to configure two objects. From
here:

- For real-world jobs such as validation, immutability and sharing, follow the [how-to guides](how-to.md).
- For exact signatures, contracts and variants, consult the [reference](reference.md).
- For the reasoning behind the private constructor and the defaults, read [About the Builder Pattern](explanation.md).
