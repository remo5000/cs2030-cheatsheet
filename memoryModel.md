## Stack and Heap Diagram Extended


#### Method call
<br>
**Before** <br>
![](https://nus-cs2030.github.io/1718-s2/figures/stack-and-heap/stack-and-heap.005.png)

  JVM creates a *stack frame* for this instance method call. This stack frame
  contains
  1. `this` reference.
  2. The method arguments. `q`
  3. Local variables within the method. _(Not shown)_

*When a class method is called, the stack frame does not contain the `this`
reference. *

**After** <br>
![](https://nus-cs2030.github.io/1718-s2/figures/stack-and-heap/stack-and-heap.006.png)

**With Primitives** <br>
![](https://nus-cs2030.github.io/1718-s2/figures/stack-and-heap/stack-and-heap.007.png)

_Note that `d` and `theta` do not point to an object but instead are
passed by value._

#### Variable capture

Consider the program below:
``` Java
class B {
  void f() {
    int x = 0;
    class A { // This is a local class
      int y = 0;
      A() {y = x + 1;}
    }
  A a = new A();
  }
}
```
Suppose that a variable b is an instance of class B, and a program calls b.f().
Sketch the content of the stack and heap immediately after the
Line A a = new A() is executed. Label the values and variables / fields clearly.
You can assume b is already on the heap and you can ignore all other content of
the stack and the heap before b.f() is called.

![Answer](https://i.snag.gy/OSH8BP.jpg)

**Variable capture**: Local class makes a copy of local
variables used from the enclosing method to within itself
This stack frame contains (due to method call):
  1. `this` reference.
  2. No method arguments.
  3. Local variables within the method. `x`

This stack frame contains (due to variable declaration):
  1. `a`, the variable initialised with a `new A()` object.

This heap contains (due to variable capture):
  1. An instance of class `A`.
    1. Captured variable `x` now part of its instance attributes.
    2. Declared variable `y` now part of its instance attributes.
