### Syntax ###

 * multiple parameter list and bracket invocation (somehow confusing IMO, one can just write params on each line)
   ```
   def f(a: A)(b:(T,U)=>V) 
   f(a) { (x,y) => x+y }
   ```
 * function type 
   * `(A, B) => C`, 
   * `A => B`   
 * function literal 
   * `(parameter: type, ...) => expression`
   * `(_ * _)` expands `(a, b) => a + b`
   
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

#### Common function names ####
  * `fold` - recursively process data type to transform it into another one. Usually receives some lambda as param.
  * `map(f:A=>B):My[B]`
  * `flatMap(f:A=>My[B]):My[B]`


#### Design guidelines - Structural recursion declarations ####

The general rule is: 
* if a method only depends on other fields and methods in a class it is a good candidate to be implemented inside the class. 
* If the method depends on other data (for example, if we needed a Cook to make dinner) consider implementing is using pattern matching outside of the classes in question. 
* If we want to have more than one implementation we should use pattern matching and implement it outside the classes.

#### Tests ####

  * `name should matchPattern { case Name("Sarah", _, _) => }`
  * 
    ```
    assertThrows[IndexOutOfBoundsException] { // Result type: Assertion
      s.charAt(-1)
    }
    ```
