## Literal Types
A literal is a more concrete sub-type of a collective type
Two sets of literal types: strings and numbers

### Literal Narrowing
The process of going from an infinite number of potential cases to a smaller, finite number of potential case.
```typescript
const a = "Hello World"; // the type of a is "Hello World" not string

let b = "Hi World"; // the type of b is string
```

### String Literal Types
combine with union types, type guards, and type aliases
```typescript
type Easing = "a" | "b" | "c";
class className {
  funcName(x: number, y: number, easing: Easing) {
    if (...) {
      ...
    }
  }
}

let instanceName = new className();
instanceName.funcName(0, 0, "a");
instanceName.funcName(0, 0, "d"); // Error: Argument of type "d" is not assignable to parameter of type "Easing"
```

### Numeric Literal Types
act the same as the string literal types
```typescript
type oneToFive = 1 | 2 | 3 | 4 | 5;

// common case is for describing config values
interface configName {
  a: number;
  b: 8 | 16 | 32;
}
```
