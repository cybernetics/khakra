[![Gitpod ready-to-code](https://img.shields.io/badge/gitpod-ready_to_code-blue?logo=gitpod&style=flat-square)](https://gitpod.io/#https://github.com/mpetuska/khakra)
[![Slack chat](https://img.shields.io/badge/kotlinlang-%23khakra-B37700?logo=slack&style=flat-square)](https://kotlinlang.slack.com/messages/khakra)
[![Version maven-central](https://img.shields.io/maven-central/v/io.github.mpetuska/khakra?logo=apache-maven&style=flat-square)](https://mvnrepository.com/artifact/io.github.mpetuska/khakra)

# KHAKRA (WIP)

Kotlin React bindings for [ChakraUI](https://chakra-ui.com/docs/getting-started)

## Using

The API is for the most part identical to the JS version, so have a look at official docs for each component's usage
samples.

### DSL

In addition to that, each component has a dedicated builder DSL taking two optional parameters - props builder lambda
and child layout builder lambda. These DSLs are also marked with `@DslMarker` (named `@KhakraDSL`) so IntelliJ should
colour them nicely for you. Sample usage:

```kotlin
fun main() {
  render(document.getElementById("root")) {
    ChakraProvider {
      Image({
        src = "https://bit.ly/2Z4KKcF"
        alt = "Rear view of modern home with pool"
      })
      Box({
        `as` = "button"
        borderRadius = "md"
        bg = "tomato"
        color = "white"
        px = 4
        h = 8
      }) {
        +"Button"
      }
    }
  }
}
```

### Utilities

If you encounter some missing properties, please report them via github issue. However, to avoid blocking your flows,
the library provides `get` and `set` operator extensions on `Any` type. This allows you to set and get any property on
any object.
> NOTE: This is completely unsafe, so make sure you know what you're doing!

```kotlin
fun RBuilder.Example() {
  Image({
    src = "https://bit.ly/2Z4KKcF" // Known property
    
    this["nonExistingProperty"] = 69 // <--------------------------------
    this["anotherNonExisting"] = this["nonExistingProperty"] // <--------
    val retrieved: Int = this["nonExistingProperty"] // Autocasted to Int
    println(this["nonExistingProperty"]) // 69
    println(this["nonExistingProperty"] == this["anotherNonExisting"]) // true
  })
}
```

## Developing

Run the sandbox to get components rendered:

```bash
./gradlew sandbox:browserDevelopmentRun -t
```

Publish to your local maven repository:

```bash
./gradlew lib:publishToMavenLocal
```
