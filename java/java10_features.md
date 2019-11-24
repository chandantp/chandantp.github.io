# Java 10 Features

### 1. Local Variable Reference
Local variables can be inferred by Java when the type is not specified. Inference does not work for method parameters, 
return type, member variables etc.
```
var message = "Hello, Java 10";
var idToNameMap = new HashMap<Integer, String>();
```
```
@Test
public void whenVarInitWithString_thenGetStringTypeVar() {
    var message = "Hello, Java 10";
    assertTrue(message instanceof String);
}
```

### 2. Unmodifiable Collections Improvements

##### copyOf()
`java.util.List, java.util.Map, java.util.Set` each got a new static method `copyOf(Collection)` which returns the 
unmodifiable copy of the given Collection.
```
@Test(expected = UnsupportedOperationException.class)
public void whenModifyCopyOfList_thenThrowsException() {
    List<Integer> copyList = List.copyOf(someIntList);
    copyList.add(4);
}
```

##### toUnmodifiable*()
`java.util.stream.Collectors` get additional methods to collect a Stream into unmodifiable List, Map or Set. Attempt to 
modify such collection would result in `java.lang.UnsupportedOperationExceptionruntime` exception.
```
@Test(expected = UnsupportedOperationException.class)
public void whenModifyToUnmodifiableList_thenThrowsException() {
    List<Integer> evenList = someIntList.stream()
      .filter(i -> i % 2 == 0)
      .collect(Collectors.toUnmodifiableList());
    evenList.add(4);
}
```

### 3. Container Awareness
JVMs are now aware of being run in a Docker container and will extract container-specific configuration instead of querying 
the operating system itself – it applies to data like the number of CPUs and total memory that have been allocated to the 
container. However, this support is only available for Linux-based platforms.



