# Using `let` to deal with optionals

Kotlin is smart enough to know that bad things (being set to null) might happen to variables
with an optional type due to naughty threads. For instance:

```kotlin
var maybeHello: String? = "Hello!"

if (maybeHello != null) {
  println(maybeHello)
}
```

This won't work as Kotlin is worried `maybeHello` could change value between the null check
and the the `println`. All objects (anything that extend `Any?`) have a `let` function 
that can help with this. The `let` function calls the passed block with the callee's value:

```kotlin
maybeHello.let {
  if (it != null) {
    println(it)
  }
}
```

Here the block passed to `let` is of type `(String?) -> Unit`. We can also combine this with
the `?` operator to give ourselves an even more succinct solution:

```kotlin
maybeHello?.let {
  println(it)
}
```

Now because of `?` the `let` function callee is now a `String` rather than a `String?`. Of course if `maybeHello`
is in fact `null` we don't need to worry as `let` will never be executed and the whole expression will simply
return `null`.

Official documentation for `let` can be found [here](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/let.html).
