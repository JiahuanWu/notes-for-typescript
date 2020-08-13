## Unions and Intersection Types

### Union Types
a value that can be one of several types  
eg: `string | number`

### Unions with Common Fields
can only access members that are common to all types in the union
```typescript
interface A {
  x(): void;
  y(): void;
}

interface B {
  x(): void;
  z(): void;
}

declare function funcName(): A | B;

let instanceName = funcName();
instanceName.x();
instanceName.y(); // error
```

### Discriminating Unions
have a single field which uses literal types which you can use to let TypeScript narrow down the possible current type.
```typescript
type A = {
  x: "la";
}

type B = {
  x: "lb";
}

type C = {
  x: "lc";
}

type D =
  | A
  | B
  | C;

function funcName(d: D): string {
  switch (d.x) {
    case "la":
      return ...;
    case "lb":
      return ...;
    case "lc":
      return ...;
  }
}
```

### Union Exhaustiveness checking
when doesn't cover all variants of the discriminated union
- turn on `--strictNullChecks` and specify a return type
- use the `never` type
  ```typescript
  function funcName(d: D): string {
    switch (d.x) {
    case "la":
      return ...;
    case "lb":
      return ...;
    case "lc":
      return ...;
    default:
      return assertNever(d) // show error if there is more type in the union
      // `assertNever` checks that `d` is type `never`
    }
  }
  ```

### Intersection Types
combines multiple types into one  
eg: `A & B`
```typescript
interface CommonName {
  x: string;
}

interface A {
  a: String;
}

type intersectionTypeA = CommonName & A;

const funcName = (data: intersectionTypeA) => {
  console.log(data.x);
  console.log(data.a);
}
```
