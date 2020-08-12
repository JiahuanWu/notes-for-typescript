## Interfaces

```typescript
interface interfaceName {
  propertyName: typeName;
  propertyName1?: typeName // ? - optional properties
}
```

### Optional Properties
- advantage: can describe these possibly available properties while still also preventing use of properties that are not part of the interface.

### Readonly Properties
Should only be modifiable when an object is first created.
- `ReadonlyArray<typeName>` - `Array<typeName>` with all mutating methods removed
- `ReadonlyArray` can not be assigned back to a normal array, needs override
  ```typescript
  let a: number[] = [1, 2, 3];
  let ro: ReadonlyArray<number> = a;
  a = ro as number[];
  ```
- Variables use `const` whereas properties use `readonly`

### Excess Property Checks
If an object literal has any properties that the "target type" doesn't have, it will throw an error.
- If an object can have some extra properties that are used in some special way, add a string index signature. `[propName: string: any`. It won't undergo excess property checks as long as you have a common property between the interface and the variable.

### Function Types
Interface for functions is like a function declaration with only the parameter list and return type given.
```typescript
interface functionName {
  (param1: typeName, param2: typeName): typeName
}
```
- The name of the parameters do not need to match.
- If you do not specify types when initializing the function, TypeScript's contextual typing can infer the argument types.

### Indexable Types
Have an index signature that describes the types we can use to index into the object, along with the corresponding return types when indexing.
- supported index signature: `number` and `string`
- a powerful way to describe the "dictionary" pattern.
  ```typescript
  interface dictionaryName {
    [index: number]: string;
    length: number;
    name: string;
  }
  ```
- make index signature `readonly`.   
`readonly [index: number]: string;`

### Class Types
- Implementing an interface (interface describes the public side of the class)
  ```typescript
  interface ClockInterface {
    currentTime: Date;
    setTime(d: Date): void;
  }

  class Clock implements ClockInterface {
    currentTime: Date = new Date();
    setTime(d: Date) {
      this.currentTime = d;
    }
    constructor(h: number, m: number) {}
  }
  ```
- Difference between the static and instance sides of classes
two types: the type of static side and the the type of the instance side. (when a class inplements an interface, only the instance side of the class is checked)

### Extending Interfaces
- An interface can extend multiple interfaces, creating a combination of all of the interfaces.

  ```typescript
  interface C extends A, B {
    ...
  }
  ```

### Hybrid Types
- An object that works as a combination of some of the types
eg: an object that acts as both a fucntion and an object
  ```typescript
  interface Counter [
    (start: number): String;
    interval: number;
    reset(): void;
  ]

  function getCounter(): Counter {
    let counter = ( function (start: number) {}) as Counter;
    counter.interval = 123;
    counter.reset = function() {};
    return counter;
  }

  let c = getCounter();
  c(10);
  c.reset();
  c.interval = 5.0;
  ```

### Interfaces Extending Classes
- When creating an interface that extends a class with private or protected members, that interface type can only be implemented by that class or a subclass of it.ß
