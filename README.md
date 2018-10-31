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

# Feel free to Contribute

You can raise a PR for contribution. Once it is reviewed it will be merged to master. You can name yourself in contributors list as well.


# Sources
https://codeburst.io/five-tips-i-wish-i-knew-when-i-started-with-typescript-c9e8609029db

# Contributors
saiprasad2595