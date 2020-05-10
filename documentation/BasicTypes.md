## Basic Types
1. Boolean
2. Number - decimal, hexadecimal, binary and octal literals
3. String
4. Array
5. Tuple - a array with a fixed number of elements whoes types are different
6. Enum - giving more friendly names to sets of numberic values
7. Any
8. Void - commonly use as the return type of a functions that do not return a value
9. Null and Undefined
10. Never - the return type for a function expression or an arrow function expression that always throws an exception or one that never returns
11. Object

### in use
```javascript
// let variableName: typeName = value;
let isDone:boolean = false;

// Array
// varibaleName - elementType[] & Array<elementType>
let list: number[] = [1, 2, 3];
let list: Array<number> = [1, 2, 3];

//Tuple
let x: [number, string] = [1, 'hello'];

// Enum
// By default, start at 0
enum Color {Red, Green, Blue}
let a: Color = Color.Red; // a = 0
// change by manually
enum Color {Red = 1, Green, Blue}
let a: Color = Color.Red; // a = 1
// convert to vanilla javascript
var Color;
(function(Color) {
    Color[Color['Red'] = 0] = 'Red';
    Color[Color['Green'] = 1] = 'Green';
    Color[Color['Blue'] = 2] = 'Blue';
})(Color || (Color = {}));
```

### Null and Undefined and Never
- By default null and undefined are subtypes of all other types. Can assign null and undefined to something like `number`.
- When using the `--strictNullChecks` flag. `null` is assignable to `null` and `any`. `undefinde` is assignable to `undefined`, `any`, and `void`.
- The  `never` type is a subtype of, and assignable to, every type; however, no type is a subtype of, or assignable to, `never`.

### Type Assertions
```javascript
let someValue: any = 'This is a string';
// <typeName>variableName
<string>someValue
// variableName as typeName
someValue as string
```