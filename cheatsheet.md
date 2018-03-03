# CS2030 Cheatsheet(s) 

## Types and Inheritence
#### Reference Conversion
#### Primitive Conversion
#### Liskov substitution principle 
If `S` is a subtype of `T`, then objects of type `T` may be replaced with objects of type `S` (i.e. an object of type `T` may be substituted with any object of a subtype `S`) without altering any of the desirable properties of `T`.

How to answer question:
  - Show the property f(`S`) that is not present in `T`, i.e f(`T`) does not hold true
  - Say that if an instance of `S` is replaced by an instance of `T`, this property will not hold
  - Thus, LSP is violated
#### Method matching
There are 3 steps Java uses to find the method to fit, and after that prioritises more accurate types.
- The first step allows for implicit widening conversions.
- The second step allows for auto-boxing and unboxing (in addition to those in step 1).
- The third step allows for variable arity methods (in addition to those in steps 1 and 2).

Within a step, if any applicable methods were found, the proceeding steps will be skipped. If multiple applicable methods were found, the most specific method will be selected. If there are more than 1 most specific methods, the method invocation is _ambiguous_ and you get a compile-time error.


## Generics & Collections
#### Generics
Suppose a class or interface `B` is a subtype of `A`, then `B<T>` is also a subtype of `A<T>`, i.e., they are covariant.

Generics, however, are _invariant_, with respect to the type parameter.  That is, if a class or interface `B` is a subtype of `A`, then neither is `C<B>` a subtype of `C<A>`, nor is `C<A>` a subtype of `C<B>`.  A parameterized type must be used with exactly with same type argument.  For instance:

Type Erasure:
- Queue<Circle> will be replaced by Queue and T will be replaced by Object.
- Queue<? extends Shape> will be replaced with Queue and T will be replaced with Shape
- The compiler also inserts type casting and additional methods to preserve the semantics of the generic type
- We cannot have both void foo(Queue<Circle> c) {} and void foo(Queue<Point> c) {} as they both get converted to void foo(Queue c) {} in compilation 
- Both Queue<Point> and Queue<Circle> will share static methods
- Queue<Point> q = new Queue() is legal
Conclusion: In runtime, the **type information is not available**.

#### Wildcards
Scenario in initialising a list:
- Assigning `A<Object>` to `A<? extends Object>`: The parameterized type is bounded by `? extends Object`.
- Assigning `A<Integer>` to `A<? super Integer>`: Java infers the type to be `Integer`. 

## hashCode, Nested Class, enum
#### Type safety (relates to Generics as well)
  - enum allows a type to be defined and used for a set of predefined constants. Using a constant other than those predefined would lead to a compilation error. In contrast, using int is not type safe since int values other than those predefined can be accidentally assigned / passed as arguments. 
  - Generics allow classes / methods that use any reference type to be defined without resorting to using the Object type. It enforce type safety by binding the generic type to a specific given type argument at compile time. Attempt to pass in an incompatible type would led to compilation error 
