# Environment

Install typescript and ts-node:

```bash
npm install -g typescript ts-node
```

Initialize NPM project directory:

```bash
npm init -y
```

Run TS compiler:

```bash
tsc
```

Compile and run TS:

```bash
ts-node file.ts
```

# Basics

Define interface:

```ts
interface InterfaceName {
    id: number;
    name: string;
    flag: boolean;
}
```

Set type for object:

```ts
const obj = data.object as InterfaceName;
```

Define variable function:

```ts
const myFunc = (id: number, name: string, flag: boolean) => {
    console.log(`Arguments: ${id} ${name} ${flag}`);
};
```

Create variable of specific type:

```ts
const today = new Date();
const year = today.getYear();
```

Create object of custom type:

```ts
const person = {
    age: 20
};
```

Define class and create object:

```ts
class Person {
}

const person = new Person();
```

# Type annotations

Define variable with type annotation (number):

```ts
const apples: number = 5;
```

Define variable with type annotation (string):

```ts
const speed: string = "fast";
```

Define variable with type annotation (boolean):

```ts
const hasName: boolean = true;
```

Null type annotation:

```ts
let nothingMuch: null = null;
```

Undefined type annotation:

```ts
let nothing: undefined = undefined;
```

Object type annotation:

```ts
const now: Date = new Date();
```

Define an array:

```ts
let colors: string[] = ["red", "green", "blue"];
let ages: number[] = [22, 33, 55];
```

Class annotation:

```ts
class Car {
}

let car: Car = new Car();
```

Object annotation:

```ts
const person: { age: number, name: string } = {
    age: 34,
    name: "John Smith"
};
```

Function type annotation (argument is type of string, returns void):

```ts
const logSomething: (error: string) => void = (error: string) => {
    console.log(error);
};

logSomething("Hello, World");
```

# Type Inference

TS can figure out type declartion information from value assigned. Variable declarion and assignment must be in same statement:

```ts
const color = "Red";
```

There is type `any` in TS. For example, `JSON.parse()` returns value of type `any`. Returned object may be of different type, and contain different types of properties depending on what is passed as argument. The idea of TS is to avoid using `any` and have as much as possible types defined to catch the errors early. But there are some cases where `any` is unavoidable.

```ts
const json = '{ "age": 22, "name": "Dick Johnson" }';
const person = JSON.parse(json);
```

Type anotations can be added to control the type of what is returned in place of `any`:

```ts
const json = '{ "age": 22, "name": "Dick Johnson" }';
const person: { age: number; name: string } = JSON.parse(json);
```

To avoid declaring `any` variable (for assigning value later), type annotation should be added: 

```ts
const words: string[] = ["one", "two", "three"];
let found: boolean;

found = false;
for (let i = 0; i < words.length; i++) {
    if (words[i] === "two")
        found = true;
}
```

In some situations it is possible to annotate variables of several different types:

```ts
let something: number | boolean = false;
something = 20;
```

Function with return type annotation:

```ts
const add = (a: number, b: number): number => {
    return a + b;
}
```

If TS can figure out what type is returned from `return` statements, return type annotation may be skipped:

```ts
const add = (a: number, b: number) => {
    return a + b;
}
```

Returning type annotation for function is recommended to use always, as this will help indicating if `return` statement is missing, or function returns incorrect type value.

Another way of defining function:

```ts
function add(a: number, b: number): number {
    return a + b;
}

console.log(add(1, 2));
```

Also another way for defining function:

```ts
const add = function(a: number, b: number): number {
    return a + b;
}
```

Funtion that does not return any value:

```ts
const log = (message: string): void => {
    console.log(message);
}
```

If function never reach end, we can indicate that with return type `never`:

```ts
const throwError = (message: string): never => {
    throw new Error(message);
}
```

Destructuring function parameter to separate variables:

```ts
const person = {
    age: 23,
    name: "Andrew"
};

const log = ({age, name}: {age: number, name: string}): void => {
    console.log("age: " + age);
    console.log("name: " + name);
};

log(person);
```

Define a function in an object:

```ts
const person = {
    age: 23,
    name: "Andrew",
    setAge(age: number): void {
        this.age = age;
    }
};

person.setAge(44);
```

Destructure and object:

```ts
const person = {
    age: 23,
    fullName: "Andrew Philips",
    earnngs: 3000
};

const { age, fullName }: { age: number, fullName: string } = person;

console.log(age, fullName);
```

Destructure from object in object:

```ts
const person = {
    age: 23,
    fullName: "Andrew Philips",
    position: {
        x: 4545,
        y: 7236
    }
};

const { position: { x, y } }: { position: { x: number; y: number }} = person;

console.log(x, y);
```

# Arrays

Array of strings:

```ts
const colors = ["green", "red", "orange"];
```

Empty array of strings:

```ts
const colors: string[] = [];
```

Two dimension array:

```ts
const colorsGroups: string[][] = [
  ["red", "green"],
  ["green", "orange"],
];
```

Working with arrays;

```ts
const colors = ["red", "green", "blue"];
const color1 = colors[2]; // access blue
const color2 = colors.pop(); // remove last item and get value (blue)
colors.push("orange"); // Add value orange
const color3 = colors[2]; // orange

// Map elements of array to other array
const things = colors.map((c: string) => {
  return (c + " thing").toUpperCase();
});
```

Multiple types in array:

```ts
const multiTypeArray: (string | number)[] = ["aaa", 222];
```

# Tuples

Tuples used when specific types with order in array must be used:

```ts
const tupleObject: [string, number, boolean] = ["Hello", 123, true];
```

# Interfaces

Definition, implementation and use as function argumet:

```ts
interface Tool {
  name: string;
  price: number;
  isBroken: boolean;
  getDescription(): string;
}

const hammer: Tool = {
  name: "Hammer 2000",
  price: 999,
  isBroken: false,
  getDescription: function (): string {
    return `This is ${this.name}`;
  },
};

const helmet: Tool = {
  name: "Orange Helmet",
  price: 22.99,
  isBroken: false,
  getDescription: function (): string {
    return `This is broken: ${this.isBroken}`;
  },
};

const logTool = (tool: Tool): void => {
  console.log(`Name: ${tool.name}`);
  console.log(`Price: ${tool.price}`);
  console.log(`Is broken: ${tool.isBroken}`);
  console.log(`Description: ${tool.getDescription()}`);
};

logTool(hammer);
logTool(helmet);
```

# Classes

Define and use a class:

```ts
class Tool {
  use(): void {
    console.log("knock knock");
  }
}

const tool = new Tool();
tool.use();
```

Inheritence and overrides:

```ts
class Tool {
  use(): void {
    console.log("knock knock");
  }
}

class Hammer extends Tool {
  use(): void {
    console.log("hammer noises");
  }
}

const tool = new Hammer();
tool.use();
```

Method modifier by default is `public`. This can be defined in following way:

```ts
class Tool {
  public use(): void {
    this.log("knock knock");
  }

  protected log(message: string): void {
    console.log(message);
  }
}

class Hammer extends Tool {
  public use(): void {
    const name = this.getName();
    this.log(`${name} noises`);
  }

  private getName(): string {
    return "hammer";
  }
}

const tool = new Hammer();
tool.use();
```

Define property:

```ts
class Toy {
  name: string = "Toy";
}
```

Define constructor and pass property value:

```ts
class Toy {
  name: string;

  constructor(name: string) {
    this.name = name;
  }
}

const toy = new Toy("Duck");
```

We can create property directly from constructor argument. In this way there is no need to define each property in class:

```ts
class Toy {
  constructor(public name: string) {}
}

const toy = new Toy("Duck");

console.log(toy.name);
```

Overriding constructors:

```ts

```
