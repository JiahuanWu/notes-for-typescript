## Classes
```typescript
class ClassName {
  propertyName: string;
  constructor(p: string) {
    this.propertyName = p;
  }
  methodName() { ... }
}
```

### Inheritance
keyword: `extends`  
classes(*subclasses*) inherit proprties and methods from base classes(*superclass*).
- Each derived class that contains a constructor function must call `super()` which will execute the constructor of the base class. 
- Have to call `super()` before accessing a property on `this` in a constructor body.
- Can override methods in the base class with methods in subclass.

### Public, Private and Protected Modifiers
- public by default
- `private`. Cannot be accessed from outside of its containing class. `#` for TypeScript 3.8.
- If a type has a `private` memeber, and the other has a `private` member that originated in the same declaration, then the two types are considered compatible. The same applies to `protected` members.
- `protected`. Can be accessed within deriving classes.

### Readonly Modifier
- `readonly`. Must be initialized at their declaration or in the contructor.

### Parameter Properties
create and initialize a member in one place
```typescript
class ClassName {
  ...
  constructor(readonly a: string) {} //`readonly` and accessibility modifier
}
```

### Accessors
- getters and setters
  ```typescript
  class ClassName {
    private p: string;

    get propertyName(): string {
      return ...
    }

    set propertyName(a: string) {
      ... //constraints
      this.p = ...
    }
  }
  ```
- notes
  1. Accessors require you to set the compiler to output ECMAScript 5 or higher. Downleveling to ECMAScript 3 is not supported.
  2. Accessors with a `get` and no `set` are automatically inferred to be `readonly`.

### Static Properties
- keyword: `static`.
- Visible on the class itself rather than on the instances. Accessed through prepending the name of the class.
  ```typescript
  class ClassName {
    static sPropertyName = ...;
    methodName(...) {
      let a  = className.sPropertyName;
      ...
    }
    constructor(...) {}
  }

  let instanceName = new ClassName(...);
  console.log(instanceName.methodName(...));
  ```

### Abstract Classes
- keyword: `abstract`. Base classes from which other classes may be derived.
- Methods within an abstract class that are marked as abstract do not contain an implementation and must be implemented in derived classes.
  ```typescript
  abstract class ClassName1 {
    constructor(...) {}
  
    normalMethodName(): void {
      console.log(...);
    }
  
    abstract abstractMethodName(): void;
  }

  class ClassName2 extends ClassName1 {
    constructor() {
      super();
    }
  
    // be implemented
    abstractMethodName(): void {
      console.log(...);
    }
    otherMethodName(): void {
      console.log(...);
    }
  }

  let a: ClassName1; // Create a reference to an abstract type
  a = new ClassName1(); // Error: Cannot create instance of an abstract class
  a = new ClassName2();
  a.normalMethodName();
  a.abstractMethodName();
  a.otherMethodName(); // Error: 'otherMethodName' does not exist on type 'ClassName1'
  ```

### Constructor Functions
```typescript
class ClassName {
  propertyName: string;

  constructor(a: string) {
    this.propertyName = a;
  }

  methodName() {
    return this.property;
  }
}

let instanceName: ClassName; // using `ClassName` as the type of instances of the class `ClassName`
instanceName = new ClassName('Hello world');
```

```typescript
class ClassName {
  static staticPropertyName = 'Hello, there';
  propertyName: string;
  methodName() {
    if (this.propertyName) {
      return 'Hello' + this.propertyName;
    } else {
      return ClassName.staticPropertyName;
    }
  }
}

let instanceName1: ClassName;
instanceName1 = new ClassName();
console.log(instancesName1.methodName()); // "Hello, there"

let instanceMaker: typeof ClassName = ClassName; // instanceMaker will hold the class itself, or said another way its constructor function
// typeof ClassName - the type of the constuctor function, contains all of the static memebers of `ClassName`
instanceMaker.staticPropertyName = 'Hey there'

let instanceName2: ClassName = new instanceMaker();
console.log(instanceName2.methodName()); // "Hey there"
```

### Using a Class as An Interface
```typescript
// class declaration creates: a type representing instances of the class and a constructor function
class ClassName {
  x: number
}

interface InterfaceName extends ClassName {
  y: number
}

let instanceName: InterfaceName = { x: 1, y: 2 };
```