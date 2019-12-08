# Constructing Collections in Java, Kotlin

### Java
##### Immutable Collections
- Java 9 provides factory methods for constructing `immutable` collections.
- Any attempt to add, set, or remove elements from these collections causes an `UnsupportedOperationException` to be thrown.
- [This article](https://docs.oracle.com/javase/9/core/creating-immutable-lists-sets-and-maps.htm) explains how immutable collections created using these factory methods are different from collections created using `Collections.unmodifiable*` wrappers and also space efficiency of such collections.

```java
var list = List.of(1,2,3)
var set = Set.of(1,2,3)
var map = Map.of("foo", "a", "bar", "b", "baz", "c")
```

##### Mutable Collections
```
???
```

### Kotlin
##### Immutable Collections
```kotlin
val numbers = listOf("one", "two", "three", "four")
val numbers = setOf(1, 2, 3, 4)
val numbersMap = mapOf("key1" to 1, "key2" to 2, "key3" to 3, "key4" to 1)
```

##### Mutable Collections
```kotlin
val numbers = mutableListOf("one", "two", "three", "four")
val numbers = mutableSetOf(1, 2, 3, 4)
val numbersMap = mutableMapOf("one" to 1, "two" to 2)
```

### Access Operations
```java
list.get(0)
$13 ==> 1

set.get(2)
|  Error:
|  cannot find symbol
|    symbol:   method get(int)

map.get("foo")
$8 ==> "a"
```

