
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

Data using the **"has-a and"** pattern is known as a product type, 

```
trait A {
  def b : B
  def c : C
}
```
**the is-a or** pattern is a sum type.
```
sealed trait A
case class B() extends A
case class C() extends A
```

** the is-a and** 

```
trait B
trait C
class A extends B with C
```

### Structural recursion declarations ###

The general rule is: 
* if a method only depends on other fields and methods in a class it is a good candidate to be implemented inside the class. 
* If the method depends on other data (for example, if we needed a Cook to make dinner) consider implementing is using pattern matching outside of the classes in question. 
* If we want to have more than one implementation we should use pattern matching and implement it outside the classes.

### Recursive algebraic data types

```
sealed trait Recursive
final case class RecursiveCase(recursion: RecursiveExample) extends RecursiveExample
final case object BaseCase extends RecursiveExample
```
