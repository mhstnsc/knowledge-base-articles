#### Patterns ####

 * `Optional.filter(_.isDefined).map(_.get)` can be replaced with `flatten`
 * **Type class** 
    ```
    trait TypeClass[A] {
        def extra(obj:A)
    }
    implicit class ExtraClassBinder[A](obj:A) {
        def extra()(implicit typeClass:TypeClass[A]) = typeClass.extra(obj)
    }
    implicit val intTypeClassInstance = new TypeClass[Int] {
        override def extra(obj: Int): Unit = print(s"This is extra for int $obj")
    }
    1.extra
    ```

#### Interesting things ####
* `map` - If the argument to flatmap returns a tuple then the result is a map, otherwise is a traverable.
* **Implicits lookup**
    * local or inherited definitions
    * imported definitions
    * definitions in the companion object of the *type class or the parameter type*
* `implicitly[A]` - get the instance of the implicit of A

#### Tests ####

 * `name should matchPattern { case Name("Sarah", _, _) => }`
 * 
    ```
    assertThrows[IndexOutOfBoundsException] { // Result type: Assertion
      s.charAt(-1)
    }
    ```
 * Ignore test with FunSuiteTest, `ignore("bla")` 

### Syntax ###

 * **function type**
   * `val x: (A, B) => R`, 
   * `val x: A => R`   
 * **function literal **
   * `(parameter: type, ...) => expression`
   * `(_ * _)` expands `(a, b) => a + b`
 * **for-comprehensions**
    ```
    for { 
       x <- a
       x = a
       if <cond>       
    } yield x    
    ```  
 * **Variancy**
    * `Foo[T]` is invariant, `Foo[+T]` is **covariant**, `F[-T]` is contravariant 
    * `TT >: T` declare a new `TT` as a supertype of `T`
    * `TT <: T` declare a new `TT` as a subtype of `T`
 * **Pattern matching**
    * `case p @ Person(_, s)` allows to capture the whole match of the pattern match 
 * Trailing colon makes things **right associative**. `0 +: list`
 * **Context bound** `[A : Context]` expands into generic type parameter `[A]` along with an implicit parameter for a `Context[A]`. Access the member with implicitly[A]
 
#### Notable function names ####
  * `fold` - recursively process data type to transform it into another one.
  * `foldLeft` - Process from left to right associativ
  * `foldright` - Process from right to left associative
  * `foreach` - Process with side effects and no return
  * `flatten` - Takes a collection of collections and returns a combined collection   
   
#### Collections ####
 * `List`
 * `Stream` - lazy eval / infinite
 * `Vector` - random access
 * `Buffer` - efficiently create a data structure an item at a time
 * `StringBuilder`
 * `LinkedList`, `DoubleLinkedList`

#### Collection operations ####
  * `:+` append, `+:` prepend, `++` concat
  * `view` - on a collection avoid creating intermediate data structures. Its worth for many elements otherwise its an overhead
  * `asJava` / `asScala` - its converting to java data structures
  * `<collection>.view` - on a collection avoid creating intermediate data structures. Its worth for many elements otherwise its an overhead
  * `<mutable>.update` / `<mutable>(index) = <val>` - to update a mutable collection
 
### Algebraic data types ###

* product type => "has-a and" pattern. E.g `Tuple`
   ```
   trait A {
     def b : B
     def c : C
   }
   ```
* sum type => "is-a or" pattern. E.g `Either`
   ```
   sealed trait A
   case class B() extends A
   case class C() extends A
   ```
   Example of **recursive data type**
   ```
   sealed trait Recursive
   final case class RecursiveCase(recursion: RecursiveExample) extends RecursiveExample
   final case object BaseCase extends RecursiveExample
   ```
* functor => A type like `F[A]` with a `map` method
* monad => A type like `F[A]` with a `map`, `flatMap`, constructor aka `point` and there are some algebraic laws that our map and flatMap operations must obey.
* "is-a and" pattern
   ```
   trait B
   trait C
   class A extends B with C
   ```
  
#### Common types ####
  * `monad` - a monad is a generic type that allows us to sequence computations while abstracting away some technicality.
  * `cats.EitherT` - 
  * `type classes` - Type classes allow us to extend existing libraries with new functionality, without using inheritance and without having access to the original library source code


#### Design guidelines - Structural recursion declarations ####

The general rule is: 
* if a method only depends on other fields and methods in a class it is a good candidate to be implemented inside the class. 
* If the method depends on other data (for example, if we needed a Cook to make dinner) consider implementing is using pattern matching outside of the classes in question. 
* If we want to have more than one implementation we should use pattern matching and implement it outside the classes.

#### Covariance ####
* We should only use covariant types where the container type is immutable. If the container allows mutation we should only use invariant types.
* sum type if we consider that C is not generic
   ```
   sealed trait A[+T]
   final case class B[T](t: T) extends A[T]
   final case object C extends A[Nothing]
   ```
* Contravariant Position Pattern
   ```
   If A of a covariant type T and a method f of A complains that T is used in a contravariant position, introduce a type TT >: T in f.
   
   case class A[+T] {
     def f[TT >: T](t: TT): A[TT]
   }
   ```

#### Not cool things (Personal opinion) ####

* Creative operator like names for collection operations like adding and removing from map (its not combining homogenous items so does not justify such a syntax). Once you see a + b one assumes its a math operation and not addition to a map so you need more context to understand it. Operators cannot be searched with find. This makes it hard to locate all the additions to maps in the code for example. 
* Using inheritance to compose functionality (by reading the code one cannot see from where things are comming, it could be down the inheritance tree). OOP was left behind long time ago. You end up eating time on making the type system work just to write a few characters less which probably makes no difference to a company well-being. 
* Augmenting with Type classes and usage of implicits. Things are popping up out of nowhere, this makes getting into a new project very slow as many things happen behind the scenes. In the end you end up showing the implicits while they could have just been made explicit. 
* Language is optimized to be concice to write but in big projects it should be optimized to be easy to get into new code. The author of the code does not need to have concise code because knows the code anyway. Code should be optimized for new people looking to new code.
* Does type classes make sense? Why not wrapping or just replacing? 
* Poor documentation of scalaz makes things hard to get into
