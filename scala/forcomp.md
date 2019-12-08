### For comprehensions - Syntactic sugar for flatMap & map

Given the following definitions...

```scala
def getX = Option(List(3))

def getY = Option(List(5))
```

The below 2 computations are the same:

```scala
getX.flatMap(x => getY.map(y => x ++ y))

val z = for {
       x <- getX
       y <- getY

     } yield x ++ y
```

Value of z:

```scala
z: Option[List[Int]] = Some(List(3, 5))
```
