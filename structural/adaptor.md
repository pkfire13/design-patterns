# Adaptor

## Applicability

Use the Adapter pattern when:
1. you want to use an existing class, and its interface does not match the one you need
2. you want to reuse several existing sublcasses that lack some common functionality that can't be added to the superclass

## Cons

- increases the overall code complexity by creating multiple additional classes and interfaces. Might be easier to just change the service class to match the client's interface.

## Example

You have a stock market monitoring app and it uses xml format from sources. You want to improve the app by integrating a smart 3rd-party analytics lib but it only takes json format. You can create an adapter that will convert the xml to json.


## Structure

### Object Adapter

1. Client: class that contains exisitng business logic
2. Client interface: protocol that other classes must follow
3. Service: a useful class
4. Adapter: a class that's able to work with both the client and the service

### Class Adapter
1. Client, Existing class (with method(data)), Service Class (with serviceMethod(specialData))
2. Adapter: extends Service Class, implements method(data)
3. specialDate = convertToServiceFormat(data)
return serviceMethod(specialData)

## Code Example

```typescript
class Target {
  public request(): string {
    return 'Target: The default target\'s behavior.';
  }
}
```

```typescript
class Adaptee {
  public specificRequest(): string {
    return '.eetpadA eht fo roivaheb laicepS';
  }
}
```

```typescript
class Adapter extends Target {
  private adaptee: Adaptee;

  constructor(adaptee: Adaptee) {
    super();
    this.adaptee = adaptee;
  }

  public request(): string {
    const result = this.adaptee.specificRequest().split('').reverse().join('');
    return `Adapter: (TRANSLATED) ${result}`;
  }
}
```

```typescript
function clientCode(target: Target) {
  console.log(target.request());
}
```

The client code supports all classes that follow the Target interface.
```typescript
const target = new Target();
clientCode(target);

const adaptee = new Adaptee();
console.log(`Adaptee: ${adaptee.specificRequest()}`);

const adapter = new Adapter(adaptee);
clientCode(adapter);
```
