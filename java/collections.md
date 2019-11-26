# Constructing Collections

Java 9 provides factory methods for constructing `immutable` collections.
Any attempt to add, set, or remove elements from these collections causes an `UnsupportedOperationException` to be thrown.

```
var list = List.of(1,2,3)
list ==> [1, 2, 3]

var set = Set.of(1,2,3)
set ==> [1, 2, 3]

var map = Map.of("foo", "a", "bar", "b", "baz", "c")
map ==> {bar=b, baz=c, foo=a}

```

### Access Operations
```
list.get(0)
$13 ==> 1

set.get(2)
|  Error:
|  cannot find symbol
|    symbol:   method get(int)

map.get("foo")
$8 ==> "a"
```

Notes
- Refer to https://docs.oracle.com/javase/9/core/creating-immutable-lists-sets-and-maps.htm for details on how immutable collections created using above factory methods are different
from collections created using `Collections.unmodifiable*` wrappers and about space efficiency.

