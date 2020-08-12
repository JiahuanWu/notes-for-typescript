## Functions

### Function Types
- add types to the function itself to add a return type

### Writing the function type
```typescript
let myAdd: (x: number, y: number) => number = function ( // paramters can be (baseValue: number, increment: number) to help with readability
  x: number,
  y: number
) : number {
  return x + y;
};
```
if the function doesn't return a value, use `void`

### Inferring the types
contextual typing (only has types on one side of the equation)
```typescript
let myAdd = function(x: number, y: number): number {
  return x + y;
}

ley myAdd2: (baseValue: number, increment: number) => number + function(x, y) {
  return x + y;
}
```

### Optional and Default Paramenters
- The number of arguments given to a function has to match the number of parameters the functions expects
- Optional parameter: 
  + adding a `?` to the end of parameters, `optParam?`
  + must follow required parameters
- Default paramters:
  + default-initialized parameters that come after required parameters are treated as optional
  + share commonality in their types
  + don't need to occur after required parameters. But need to pass `undefined` when coming before a required parameter

### Rest Parameters
treated as a boundless number of optional parameters
```typescript
function buildName(firstName: string, ...restOfName: string[]) {
  return firstName + "" + restOfName.join(" ");
}

// the ellipsis is also used in the type of the function with rest parameters
let buildNameFun: (fname: string, ...rest: string[]) => string = buildName;
```

### This
a variable that's set when a function is called.
a top-level non-method syntax call like this will use `window` for `this`(Note: under strict mode, `this` will be `undefined`)

- This and arrow functions
  Arrow functions capture the `this` where the function is created rather than where it is invoked
- This parameters
  Because `this` comes from the function expression inside the object literal, `this.kyeName` is `any`. To fix this, provide an explicit `this` parameter
  ```typescript
  function f(this: void) {
    // make sure `this` is unusable in this standalone function
  }
  // in instance
  f: function (this: interfaceName) {
    return () => {
      this.keyName...
    }
  }
  ```
- This parameters in callbacks
  When passing functions to a library that will later call them, `this` will be `undefined`.

### Overloads
use overloads to return different types of objects based the arguments passed in
```typescript
//eg:
// two overloads
function funcName(x: { a: string; b: number }[]): number;
function funcName(x: number): { a: string; b: number };
function funcName(x: any): any {
  if (...) {
    return ...
  } else if (...) {
    return ...
  }
}
```
