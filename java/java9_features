
# Java 9 Features

### 1. Java Platform Module System

The new module system enables modular JAR files to declare what packages are exported by the module and what packages it 
requires. Modular JAR files contain an additional module descriptor in which dependencies on other modules 
are specified through`requires` statements. Also, `exports` statements control which packages are accessible to 
other modules. All non-exported packages are encapsulated in the module by default. 

Example of a module descriptor which lives in `module-info.java`:

```
module blog {
  exports com.pluralsight.blog;

  requires cms;
}
```

### 2. Linking
When you have modules with explicit dependencies, and a modularized JDK, your application modules now state their dependencies 
on other application modules and on the modules it uses from the JDK. This can be used to create a minimal runtime environment, 
containing just those modules necessary to run your application using the new `jlink` tool in Java 9. Instead of shipping your 
app with a fully loaded JDK installation, you can create a minimal runtime image optimized for your application.

### 3. JShell
The Reat-Evaluate-Print-Loop (REPL) finally comes to Java in the form of JShell.

### 4. Improved Javadoc
Javadoc now includes search right in the API documentation itself. The Javadoc output is now HTML5 compliant. Also, every Javadoc 
page includes information on which JDK module the class or interface comes from.

### 5. Stream API Improvements
- Four new methods added to the Stream interface: `dropWhile`, `takeWhile`, `ofNullable`. 
- The iterate method gets a new overload, allowing you to provide a Predicate on when to stop iterating. The second argument 
is a lambda that returns true until the current element in the IntStream becomes 100. This simple example therefore prints the 
integers 1 until 99 on the console.
```
IntStream.iterate(1, i -> i < 100, i -> i + 1).forEach(System.out::println);
```
- Integration between Optional and Stream has been improved. It's now possible to turn an Optional object into a (possibly 
empty) Stream with the new `stream` method on Optional. This is especially useful when composing complex Stream pipelines.
```
Stream<Integer> s = Optional.of(1).stream();
```

### 6. Private Interface methods
ava 8 brought us default methods on interfaces. An interface can now also contain behavior instead of only method signatures. 
But what happens if you have several default methods on an interface with code that does almost the same thing? Normally, 
you'd refactor those methods to call a private method containing the shared functionality. But default methods can't be 
private. Creating another default method with the shared code is not a solution, because this helper method becomes part 
of the public API. With Java 9, you can add private helper methods to interfaces to solve this problem:
```
public interface MyInterface {

    void normalInterfaceMethod();

    default void interfaceMethodWithDefault() {  init(); }

    default void anotherDefaultMethod() { init(); }

    // This method is not part of the public API exposed by MyInterface
    private void init() { System.out.println("Initializing"); }
}
```

### 7. HTTP/2 Support
A new way of performing HTTP calls arrives with Java 9. This much overdue replacement for the old `HttpURLConnection` API 
also supports WebSockets and HTTP/2 out of the box. Note however that the new HttpClient API is delivered as a so-called 
`incubator module` in Java 9.

### 8. Multi-release JAR's
Multi-release JAR feature allows you to create alternate versions of classes that are only used  when 
running the library on a specific Java version.

```
multirelease.jar
├── META-INF
│   └── versions
│       └── 9
│           └── multirelease
│               └── Helper.class
├── multirelease
    ├── Helper.class
    └── Main.class
```
In this case, multirelease.jar can be used on Java 9, where instead of the top-level multirelease.Helper class, the 
one under `META-INF/versions/9` is used. This Java 9-specific version of the class can use Java 9 features and 
libraries. At the same time, using this JAR on earlier Java versions still works, since the older Java versions only
see the top-level Helper class.
