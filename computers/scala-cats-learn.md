
The usual imports (seems like importing all breaks the semigroup)

```
import cats.<bla>
import cats.syntax.<bla>._
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

## Classes ## 
* `Show` Custom printers for classes - `Show.show`
* `Eq`,`===`,`=!=` because in scala `==` compares any objects but cats makes it type safe
  * `Eq.instance` to build a custom Eq




