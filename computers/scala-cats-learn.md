
The usual imports (seems like importing all breaks the semigroup)

```
import cats.<bla>
import cats.syntax.flatmap._
import cats.syntax.functor._ .  // gives map
import cats.implicits.int._
import cats.implicits.string._
```

## Concepts ##
* `Monoid` - models combining items of same type in an **associative** and has an **identity** (`a combine i = a`)
  ```
  trait Monoid[A] {
    def combine(x: A, y: A): A
    def empty: A
  }
  ```
* `Semigroup` - Monoid without identity
  ```
  trait Semigroup[A] {
    def combine(x: A, y: A): A
  }
  ```
* `Functor` - anything with a map (good for sequencing ops)
  ```
  trait Functor[F[_]] {
    def map[A, B](fa: F[A])(f: A => B): F[B] // appends to the chain
    def contramap[C](f: C => A): F[C] // prepends to the chain
    def imap[A, B](fa: F[A])(f: A => B)(g: B => A): F[B] // prepends and appends to the chain
  }
  ```
* `Contravariant` functors, with their contramap method, represent the ability to “prepend” functions to a function-like context. Successive calls to `contramap` sequence these functions in the opposite order to `map.`
  ```
  trait Functor[F[_]] {
    def contramap[C](f: C => A): F[C] // prepends to the chain
  }
  ```  
* `Invariant` functors, with their `imap` method, represent bidirectional transformations.
  ```
  trait Functor[F[_]] {
    def imap[A, B](fa: F[A])(f: A => B)(g: B => A): F[B] // prepends and appends to the chain
  }
  ```
* `def pure[A](v: A): Monad[A]` - takes a pure value and wraps it.

## Higher Kinded Types ##
Kinds are like types for types. They describe the number of “holes” in a type

## Classes ## 
* `Show` Custom printers for classes - `Show.show`
* `Eq`,`===`,`=!=` because in scala `==` compares any objects but cats makes it type safe
  * `Eq.instance` to build a custom Eq
* `Functor`
* `Contravariant`
* `Invariant`
* `Eval` - wrapps a computation as a monad and captures the evaluation semantics (lazy, eager, memoised). The `map` and `flatmap` methods are trampolined (stack overload safe by moving stack to heap)
* `Writer[W, R]` - Monad used to record a log for the computation. `W` is the log type and `R` is the result. 
* `Reader[

## Useful functions ##
* `Either.asRight[A]` - e.g `1.asRight[Int]






