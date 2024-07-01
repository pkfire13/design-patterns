# Factory Method

## Applicability

Use the Factory Method pattern when:
1. you don't know beforehand the exact types and dependencies of the objects your code should work with
2. you want to provide users of your library or framework with a way to extend its internal components
3. you want to save system resources by reusing existing objects instead of rebuilding them each time

## Example
A logistic management app handle transportation goods and the first version uses trucks for transportation. Currently, you create a new Truck object and execute a deliver method. The app business needs to add ship as a new transportation method.

### Solution
Create a Logistic class the has createTransport method. Create 2 subclasses for RoadLogistic and SeaLogistic. Each subclass has its own createTransport method that returns a new Truck or Ship object.

Then create an interface "Transport" with the deliver method. Apply the interface to Truck and Ship classes so that when you call deliver method, it will execute the correct deliver method.

## Structure

1. Product Interface <- Concrete Product A,B,...
2. Creator Abstract Class <- Concrete Creator A,B,...

## Code Example

Creator
```typescript
abstract class Creator {
  public abstract factoryMethod(): Product;

  public someOperation(): string {
    const product = this.factoryMethod();
    return `Creator: The same creator's code has just worked with ${product.operation()}`;
  }
}

class ConcreteCreator1 extends Creator {
  public factoryMethod(): Product {
    return new ConcreteProduct1();
  }
}

class ConcreteCreator2 extends Creator {
  public factoryMethod(): Product {
    return new ConcreteProduct2();
  }
}
```

Product
```typescript
interface Product {
  operation(): string;
}

class ConcreteProduct1 implements Product {
  public operation(): string {
    return '{Result of the ConcreteProduct1}';
  }
}

class ConcreteProduct2 implements Product {
  public operation(): string {
    return '{Result of the ConcreteProduct2}';
  }
}
```

Client Code
```typescript
function clientCode(creator: Creator) {
  console.log('Client: I\'m not aware of the creator\'s class, but it still works.');
  console.log(creator.someOperation());
}

console.log('App: Launched with the ConcreteCreator1.');
clientCode(new ConcreteCreator1());
console.log('');

console.log('App: Launched with the ConcreteCreator2.');
clientCode(new ConcreteCreator2());
```
