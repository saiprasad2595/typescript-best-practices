# Typescript Best Practices

![Alt text](./typescript_logo.png "TypeScript")

For better typescripting you need to maintain better tsconfig.json file and tslint.json files.

Below are the few strict configurations you need to follow.

> 1) Strict Configuration

 Enable these flags in tsconfig.json file.
```
{
  "forceConsistentCasingInFileNames": true,
  "noImplicitReturns": true,
  "strict": true,
  "noUnusedLocals": true,
}
```
- strictNullChecks

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
### Getter / Setter

Instead of :
```
declare function duration(value?: number): any;
```
better to do:
```
declare function duration(): number;
declare function duration(value: number): void;
```
### Fluent:

Pretty self explanatory:
```
interface Something {
   foo(): Something;
   bar(): Something;
}
```
# Feel free to Contribute

You can raise a PR for contribution. Once it is reviewed it will be merged to master. You can name yourself in contributors list as well.


# Sources
https://codeburst.io/five-tips-i-wish-i-knew-when-i-started-with-typescript-c9e8609029db

# Contributors
saiprasad2595
