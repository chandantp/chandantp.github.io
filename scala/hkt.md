### Type Constructors
Type constructors can be thought of as functions that take a type as an argument instead of a value.

*Example:*
```
List[+A] is a type constructor

Here, A is a type variable
```

### Higher Kinded Types (HKT's)
A set of types of the same kind are referred to as HKTs.
For example, there can be several types of lists. Hence, list can be considered a HKT.

There is also an order associated with the HKT.

In fact, List is considered as a higher kinded type of the 1st order.

```scala
scala> :k List
List's kind is F[+A]

scala> :k -v List
List's kind is F[+A]
* -(+)-> *

This is a type constructor: a 1st-order-kinded type.
```

### Functors
Functor is a map function that, given 
- a function 'f: A => B' and 
- a value wrapped in a context 'F[A]'

can unwrap the value inside F[A], apply the function f to the value to generate value of type B and wrap the same inside context F to generate F[B]

```scala
scala> trait Functor[F[_]] {
     |   def map[A,B](fa: F[A])(f: A => B): F[B]
     | }
defined trait Functor

scala> :k -v Functor
Functor's kind is X[F[A]]
(* -> *) -> *

This is a type constructor that takes type constructor(s): a higher-kinded type.
```

Functor is a higher kinded type of the 2nd order as it's type constructor takes type constructor as argument.


### Monads
Monad is a transformation function that given f: A => F[B] and F[A], applies the function f to the value in F[A] and wraps the result in the context F i.e. F[F[B]] which is then further flattened get F[B].

```scala
scala> trait Monad[F[_]] {
     |   def flatMap[A,B](fa: F[A])(f: A => F[B]): F[B]
     | }
defined trait Monad

scala> :k -v Monad
Monad's kind is X[F[A]]
(* -> *) -> *

This is a type constructor that takes type constructor(s): a higher-kinded type.
```

### Applicatives
Applicative is a transformation construct that given a function wrapped inside a context F[A => B] and value wrapped inside a context F[A], unwraps both the function & value, applies the function to the value to generate a type B value and wraps it inside the context F to generate F[B]

```scala
scala> trait Applicative[F[_]] {
     |   def apply[A,B](fa: F[A])(fab: F[A => B]): F[B]
     | }
defined trait Applicative

scala> :k -v Applicative
Applicative's kind is X[F[A]]
(* -> *) -> *

This is a type constructor that takes type constructor(s): a higher-kinded type.
```

##### References
- https://thedet.wordpress.com/2012/04/28/functors-monads-applicatives-can-be-so-simple/
- https://thedet.wordpress.com/2012/05/04/functors-monads-applicatives-different-implementations/

