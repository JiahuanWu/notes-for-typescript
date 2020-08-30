## Generics
Being able to create a component that can work over a variety of types rather than a single one

### Hello World of Generics
- `type variable` - a special kind of variable that works on types rather than values

  ```typescript
  // `identity` function is generic
  function identity<T>(arg: T): T { // T - type variable
    return arg;
  }

  // one way
  let output = identity<string>("myString");

  // the other
  // using *type argument inference* - the compiler sets the value of `T` automatically based on the type of the argument passed in
  let output = identity("myString");
  ```

### Generic Types
```typescript
function identity<T>(arg: T): T {
  return arg;
}

let myIdentity: <T>(arg: T) => T = identity; // can use a different name for the generic type parameter(T) in the type

// write the generic type as a call signature of an object literal type
let myIdentity: { <T>(arg: T): T } = identity;

// move the object literal to an interface
interface GenericIdentityFn<T> {
  (arg: T): T; 
}
let myIdentity: GenericIdentityFn<number> = identity;
```

### Generic Classes
only generic over their instance side rather than their static side
```typescript
class GenericNumber<T> {
  propertyName: T;
  functionName: (x: T, y: T) => T;
}

let myGenericNumber = new GenericNumber<number>();
myGenericNumber.propertyName = 0;
myGenericNumber.add = function(x, y) {};
```

### Generic Constraints
```typescript
interface constraintName{
  propertyName: typeName; // length: number;
}

function functionName<T extends constraintName>(arg: T): T {
  console.log(arg.propertyName); // will results in error if there is no constrait as not each type T has the 'propertyName' property
  return arg;
}

functionName(3); // Argument of type 'number' is not assignable to parameter of type 'constraintName'
```

using type parameters
```typescript
function functionName<T, K extends keyof T>(obj: T, key: K) {
  return obj[key];
}
let x = { a: 1, b: 2 };
functionName(x, 'a'); // => 1
functionName(x, 'z'); // error
```

### Using Class Types in Generics
when creating factories using generics, it is necessary to refer to class type by their constructor functions.
```typescript
function create<T>(c: { new (): T }): T {
  return new c();
}
```
