# Typescript Best Practices

![Alt text](./typescript_logo.png "TypeScript")

For better typescripting you need to maintain better tsconfig.json file and tslint.json files.

Below are the few strict configurations you need to follow.

> ## Strict Configuration

 Enable these flags in tsconfig.json file.
```
{
  "forceConsistentCasingInFileNames": true,
  "noImplicitReturns": true,
  "strict": true,
  "noUnusedLocals": true
}
```
- #### strictNullChecks

```
interaface Foo{
    bar : string;
}

const fn = (foo? Foo) => foo.bar;
```
In the above example, function fn as an optional parameter that means it has the chances of getting value as undefined. Instead we can make the functions as below.

```
const fn = (foo: Foo | undefined) => foo.bar;
```
By using this we can overcome the runtime errors

```
TypeError: Cannot read property 'foo' of undefined
```

```
- #### noImplicitAny
```
You need to turn on the rule in tslint.json

```
no-any: true
```

This helps in showing the error if you dont define any type for function or variables. And it is strictly asked to define the type. If you dont define any type for the function or variable defautly it takes 'any' type which is considered as evil.

> ## instanceof operator
```
  class A {
    hello() {
      console.log('hello');
    }
  }

  class B {
    bonjour() {
      console.log('bonjour');
    }
  }

  const myFunction2 = (sayHello: A | B) => {
    if (sayHello instanceof A) {
      sayHello.hello();
    } else {
      sayHello.bonjour();
    }
  }

  myFunction2(new A());
```

The above code consoles 'hello'. In this example we are able to infer classes in if and else statements.

### Return Types of Callbacks
Don’t use the return type any for callbacks whose value will be ignored:
```
/* WRONG */
function fn(x: () => any) {
    x();
}
```
Do use the return type void for callbacks whose value will be ignored:
```
/* OK */
function fn(x: () => void) {
    x();
}
```

### Overloads and Callbacks
Don’t write separate overloads that differ only on callback arity:
```
/* WRONG */
declare function beforeAll(action: () => void, timeout?: number): void;
declare function beforeAll(action: (done: DoneFn) => void, timeout?: number): void;
```
Do write a single overload using the maximum arity:
```
/* OK */
declare function beforeAll(action: (done: DoneFn) => void, timeout?: number): void;
```

## Function Overloads
### Ordering
Don’t put more general overloads before more specific overloads:
```
/* WRONG */
declare function fn(x: any): any;
declare function fn(x: HTMLElement): number;
declare function fn(x: HTMLDivElement): string;

var myElem: HTMLDivElement;
var x = fn(myElem); // x: any, wat?
```
Do sort overloads by putting the more general signatures after more specific signatures:
```
/* OK */
declare function fn(x: HTMLDivElement): string;
declare function fn(x: HTMLElement): number;
declare function fn(x: any): any;

var myElem: HTMLDivElement;
var x = fn(myElem); // x: string, :)
```
# Feel free to Contribute

You can raise a PR for contribution. Once it is reviewed it will be merged to master. You can name yourself in contributors list as well.


# Sources
https://codeburst.io/five-tips-i-wish-i-knew-when-i-started-with-typescript-c9e8609029db

# Contributors
saiprasad2595
