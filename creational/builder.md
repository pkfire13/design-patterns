# Builder

## Applicability

Use the Builder pattern when:
1. to get rid of a "telescopic constructor" (a constructor with many parameters)
e.g. `new House(1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20)`
2. you want your code to be able to create different representations of some product (for example, stone and wooden houses)
3. to construct Composite trees or other complex objects

## Example

How to create a House object, can havestatues, gardens, pools, and garages.

### Solution

extract the object construction code out of its own class and move it to separate objects called builders.

### Structure

e.g you can even have a Director class that will extract a series of call to the builder steps.

1. Builder Interface (buildStepA, B, reset()) <- Concrete Builder A,B,...
2. Product: the resulting object of the builder
3. Director: optional, if you want to have a series of call to the builder steps. Only responsible for executing the building steps in a particular sequence.

## Code Example

Builder
```typescript
interface Builder {
  productPartA(): void;
  productPartB(): void;
  productPartC(): void;
}

class ConcreteBuilder1 implements Builder {
  private product: Product1;

  constructor() {
    this.reset();
  }

  pubolic reset(): void {
    this.product = new Product1();
  }

  public productPartA(): void {
    this.product.parts.push('PartA1');
  }

  public productPartB(): void {
    this.product.parts.push('PartB1');
  }

  public productPartC(): void {
    this.product.parts.push('PartC1');
  }

  public getProduct(): Product1 {
    const result = this.product;
    this.reset();
    return result;
  }
}
```

Product
```typescript
class Product1 {
  public parts: string[] = [];

  public listParts(): void {
    console.log(`Product parts: ${this.parts.join(', ')}\n`);
  }
}
```

Director
```typescript
class Director {
  private builder: Builder;

  public setBuilder(builder: Builder): void {
    this.builder = builder;
  }

  public buildMinimalViableProduct(): void {
    this.builder.productPartA();
  }

  public buildFullFeaturedProduct(): void {
    this.builder.productPartA();
    this.builder.productPartB();
    this.builder.productPartC();
  }
}
```

Client
```typescript
function clientCode(director: Director) {
  const builder = new ConcreteBuilder1();
  director.setBuilder(builder);

  console.log('Standard basic product:');
  director.buildMinimalViableProduct();
  builder.getProduct().listParts();

  console.log('Standard full featured product:');
  director.buildFullFeaturedProduct();
  builder.getProduct().listParts();

  console.log('Custom product:');
  builder.productPartA();
  builder.productPartC();
  builder.getProduct().listParts();
}

const director = new Director();
clientCode(director);
```
