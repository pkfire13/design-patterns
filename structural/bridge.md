# Bridge

## Applicability

Use the Bridge pattern when:
1. you want to divide and organize a monolithic class that has several variants of some functionality (for example, if the class can render objects in different ways)
2. you need to extend a class inseveral orthogonal (independent) dimensions
3. you need to be able to switch implementations at runtime

## Cons
- might make the code more complex by applying the pattern to a highly cohesive class

## Example

You have a Shape class with a Circle and Square subclass, you want to extend this class hierarchy to have colors, so you create a Red and Blue subclass BUT you end up with 4 classes: RedCircle, BlueCircle, RedSquare, BlueSquare.

## Structure

1. Abstraction: provides high-level control logic
2. Implementation: declares the interface for the implementation classes
3. Concrete Implementation: contains platform-specific code

## Example Code

```typescript
class Abstraction
  protected implementation: Implementation

  constructor(implementation: Implementation) {
    this.implementation = implementation
  }

  public operation(): string {
    const result = this.implementation.operationImplementation()
    return `Abstraction: Base operation with:\n${result}`
  }
}
```

```typescript
class ExtendedAbstraction extends Abstraction
  public operation(): string {
    const result = this.implementation.operationImplementation()
    return `ExtendedAbstraction: Extended operation with:\n${result}`
  }
```

```typescript
interface Implementation {
  operationImplementation(): string
}
```

```typescript
class ConcreteImplementationA implements Implementation {
  public operationImplementation(): string {
    return 'ConcreteImplementationA: Here\'s the result on the platform A.'
  }
}

class ConcreteImplementationB implements Implementation {
  public operationImplementation(): string {
    return 'ConcreteImplementationB: Here\'s the result on the platform B.'
  }
}
```

```typescript
function clientCode(abstraction: Abstraction) {
  console.log(abstraction.operation())
}

let implementation = new ConcreteImplementationA()
let abstraction = new Abstraction(implementation)
clientCode(abstraction)

implementation = new ConcreteImplementationB()
abstraction = new ExtendedAbstraction(implementation)
clientCode(abstraction)
```
