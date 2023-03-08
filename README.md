# TypeScript


## Kurulum

```
npm install -g typescript
```

### Downleveling

TypeScript varsayılan olarak **ES3**'e göre kodu çevirir.
Eğer daha yüksek bir sürüm hedefliyorsak `tsc --target es2015 hello.ts` komutunu kullanabiliriz.

- Detaylı bilgi: [target](https://www.typescriptlang.org/tsconfig#target)

Güncel tarayıcıların büyük bir çoğunluğu ES6'yı desteklediği için varsayılan hedef bu sürüme yükseltilebilir.

- Detaylı bilgi: [ES6 tarayıcı uyumu](https://caniuse.com/es6)

### Explicit Types

Değişkenlerin türlerininin belirtilmesi

```ts
function greet(person: string, date: Date) {
  console.log(`Hello ${person}, today is ${date.toDateString()}!`);
}
```

Tüm türler: `string`, `number`, `boolean`, `number[]`, `string[]`, `any`

#### Type Annotations on Variables

Değişkenleri tanımlarken değerini verebiliriz.

```ts
let myName: string = "Alice";
```

#### Return Type Annotations

Bir fonksiyonda return edilen değerin türünü belirtebiliriz.

```ts
function getFavoriteNumber(): number {
  return 26;
}
```

#### Optional Object Properties

Opsiyonel bir parametre var ise bunu `?` ile belirtebiliriz. 

```ts
function printName(obj: { first: string; last?: string }) {
  // ...
}

// Both OK
printName({ first: "Bob" });
printName({ first: "Alice", last: "Alisson" });
```

#### Union Types

Değişkenlere birden çok tür atanabilir.

```ts
function printId(id: number | string) {
  console.log("Your ID is: " + id);
}
// OK
printId(101);
// OK
printId("202");
// Error
printId({ myID: 22342 });
```

Bu şekilde birden çok tür atanan değişkenlerde işlem yaparken `typeof` ile tip kontrolü yapmalıyız.

```ts
function printId(id: number | string) {
  if (typeof id === "string") {
    // In this branch, id is of type 'string'
    console.log(id.toUpperCase());
  } else {
    // Here, id is of type 'number'
    console.log(id);
  }
}
```

#### Type Aliases

```ts
type Point = {
  x: number;
  y: number;
};
 
// Exactly the same as the earlier example
function printCoord(pt: Point) {
  console.log("The coordinate's x value is " + pt.x);
  console.log("The coordinate's y value is " + pt.y);
}
 
printCoord({ x: 100, y: 100 });
```

```
type ID = number | string;
```

`type` yerine `interface`te kullanılabilir (Tamamen aynı şey değildir fakat büyük ölçüde benzerdir):

```ts
interface Point {
  x: number;
  y: number;
}
```

- Detaylı bilgi: [type vs interface](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#differences-between-type-aliases-and-interfaces)

#### Literal Types

```ts
function printText(s: string, alignment: "left" | "right" | "center") {
  // ...
}
printText("Hello, world", "left");
printText("G'day, mate", "centre"); // Hata
```

```ts
function compare(a: string, b: string): -1 | 0 | 1 {
  return a === b ? 0 : a > b ? 1 : -1;
}
```

```ts
interface Options {
  width: number;
}
function configure(x: Options | "auto") {
  // ...
}
configure({ width: 100 });
configure("auto");
configure("automatic"); // Hata
```

#### Discriminated unions

```ts
interface Shape {
  kind: "circle" | "square";
  radius?: number;
  sideLength?: number;
}

function handleShape(shape: Shape) {
  // ...
}
```

```ts
interface Circle {
  kind: "circle";
  radius: number;
}
 
interface Square {
  kind: "square";
  sideLength: number;
}
 
type Shape = Circle | Square;
```

#### Object Types

```ts
function greet(person: { name: string; age: number }) {
  return "Hello " + person.name;
}
```

```ts
type Person = {
  name: string;
  age: number;
};
 
function greet(person: Person) {
  return "Hello " + person.name;
}
```
