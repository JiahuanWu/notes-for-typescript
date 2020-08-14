## Enums
A set of named constants. Keyword: `enum`.

### Numeric Enums
Auto-incremented. If not initialize the first one, it will start at `0`.
```typescript
enum EnumName {
  a = 1,
  b, // will be 2
  c, // will be 3
  d // will be 4
}
```
Notes: enums without initializers either need to be first, or have to come after numeric enums initialized with numeric constants or other constants enum members.

### String Enums
Each memeber has to be constant-initialized with a string literal, or with another string enum member.

### Heterogeneous Enums (not advised)
Can be mixed with string and numeric memebers.

### Computed and Constant Memebers
- Constant:
  + It is the first member in the enum and it has no initializer, in which case it's assigned the value `0`;
  + It does not have an initializer and the preceding enum member was a `numeric` constant.
  + The enum member is initialized with a constant enum expression.  
  constant enum expression:
    1. a literal enum expression (basically a string literal or a numeric lietal)
    2. a reference to previously defined contant enum member (which can originate from a difference enum)
    3. a parenthesized constant enum expression
    4. one of the `+`, `-`, `~` unary operators applied to constant enum expression
    5. `+`, `-`, `*`, `/`, `%`, `<<`, `>>`, `>>>`, `&`, `|`, `^` binary operators with constant enum expressions as operands
   
- Computed: other cases.

### Union Enums and Enum Member Types
- literal enum member is a constant enum member with no initialized value, or with values that are initialized to
  + any string literal
  + any numeric literal
  + a unary minus applied to any numeric literal
- enum member types
  ```typescript
  enum EnumName {
    A,
    B
  }

  interface InterfaceName {
    x: EnumName.A;
    y: string;
  }

  let instanceName: InterfaceName = {
    x: EnumName.B, // Error
    y: '..'
  }
  ```
- union enums
the type system is able to leverage the fact that it knows the exact set of values that exist in the enum itself.

### Enums at Runtime
Enums are real objects that exist at runtime

### Enums at Compile Time
- use `keyof typeof` to get a Type that represents all Enum keys as strings
  ```typescript
  enum EnumName {
    A,
    B,
    C
  }

  type TypeName = keyof typeof EnumName; // equals type TypeName = 'A' | 'B' | 'C'
  ```

- Reverse mappings (only numeric enums)
  ```typescript
  enum EnumName {
    A
  }

  let a = EnumName.A;
  let nameOfA = Enum[a]; // "A"
  ```

- **Const** enums  
`const enum EnumName {}`  
can only use constant enum expressions and are completely removed during compilation.

### Ambient enums
used to describe the shape of already existing enum types
```typescript
declare enum EnumName {
  A = 1,
  B,
  C = 2
}
```

diffence between ambient and non-ambient enums:
- ambient (and non-const) enum member that does not have initializer is *always* considered computed.
- non-ambient enum member that does not have initializer is considered constant if its preceding enum member is considered constant.
