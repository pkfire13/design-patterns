# Prototype

## Applicability

Use the Prototype pattern when:
1. your code shouldn't depend on the concrete classes of objects that you need to copy.
2. you want to reduce the number of subclasses that only differ in the way they initialize their respective objects.

## Example

You want to create an exact copy of an object. You create a new object and copy their values over to the new object. BUT, some object fields may be private and not visible.

### Solution

Prototype patterns allows you to delegate the cloning process by declaring a common interface for all objects that support cloning. This interface allows you to clone an object without knowing its concrete class.
Implement the `clone` method in the prototype interface.

## Structure

1. Interface `Prototype` declares a method for cloning itself.

## Cons
1. cloning complex objects that have circular references can be tricky.


## Example Code
