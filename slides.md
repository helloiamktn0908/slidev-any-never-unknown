---
theme: penguin
title: "any and never and unknown"
download: true
background: https://source.unsplash.com/collection/94734566/1920x1080
class: "text-center"
colorSchema: "dark"
favicon: "./about.jpg"
lineNumbers: false
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
drawings:
  persist: false
layout: presenter
presenterImage: "./about.jpg"
fonts:
  sans: "Poppins,Noto Sans JP"
  # default
  weights: "200,400,600"
  # import italic fonts, default `false`
  italic: false
---

<h1 class="h1">anyとneverとunknown</h1>

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    Press Space for next page <carbon:arrow-right class="inline"/>
  </span>
</div>

<div class="abs-br m-6 flex gap-2">
  <a href="https://github.com/helloiamktn0908" target="_blank" alt="GitHub"
    class="text-xl icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

<style>
  
.h1 {
font-family: Poppins, Noto Sans JP;
font-weight: 600;
font-style: normal;
}
</style>

---

<h1 class="h1">any型とは</h1>

どのような値でも代入できる。

```ts {all|1-2|1-3|1-4|all}
let value: any;
value = 1; //OK
value = 'string'; //OK
value = { name: "object" }; //OK 
```

<br>
<br>

<style>
.h1 {
font-family: Poppins, Noto Sans JP;
font-weight: 600;
font-style: normal;
}
</style>

---

<h1 class="h1">any型とは</h1>

コンパイラーが型チェックを行わないため、実行してからエラーになる。

```ts
const str: any = 123;
str.toLowerCase(); //TypeError: str.toLowerCase is not a function
```

<br>
<br>

<style>
.h1 {
font-family: Poppins, Noto Sans JP;
font-weight: 600;
font-style: normal;
}
</style>

---

<h1 class="h1">どんな時に使う？</h1>

- どんな時でも使える。
- が、any型の濫用はJavaScriptを書いていることと同じなのでできるだけ使わない。

<br>
<br>

<style>
.h1 {
font-family: Poppins, Noto Sans JP;
font-weight: 600;
font-style: normal;
}
</style>

---


<h1 class="h1">unknown型とは</h1>

どのような値でも代入できる(any型と同じ)。

```ts {all|1-2|1-3|1-4|all}
let value: unknown;
value = 1; //OK
value = 'string'; //OK
value = { name: "object"}; //OK 
```

<br>
<br>

<style>
.h1 {
font-family: Poppins, Noto Sans JP;
font-weight: 600;
font-style: normal;
}
</style>

---

<h1 class="h1">unknown型とany型の違い</h1>

unknown型の変数をunknownとany以外の変数に代入することはできない。<br/>
型ガードがあれば代入可能。<br/>


```ts
let a: unknown;            // unknown 型変数
let b1: unknown = a;       // unknown 型は unknown 型に代入可能
let b2: any = a;           // unknown 型は any 型に代入可能
let b3: number = a;        // ERROR: TS2322: unknown 型は number 型に代入不可能
let b4: object = a;        // ERROR: TS2322: unknown 型は object 型に代入不可能
let b5: {} = a;            // ERROR: TS2322: unknown 型は「{}」型に代入不可能
let b6: undefined = a;     // ERROR: TS2322: unknown 型は undefined 型に代入不可能
let b7: never = a;         // ERROR: TS2322: unknown 型は never 型に代入不可能
```

<br>
<br>

<style>
.h1 {
font-family: Poppins, Noto Sans JP;
font-weight: 600;
font-style: normal;
}
</style>

---

<h1 class="h1">unknown型とany型の違い</h1>

unknwon型は実行ができない。

```ts {1-2|3-4|5-10|all}
const unknown1 = 0.8;
console.log(unknown1.toFixed()); //Object is of type 'unknown'.
const unknown2 = "riibekuntoofuro"; 
console.log(unknown2.length) //Object is of type 'unknown'.
const unknown3 = {
  x: 0,
  y: 1,
  name: "origin",
};
console.log(unknown3.name) //Object is of type 'unknown'.
```

<br>
<br>

<style>
.h1 {
font-family: Poppins, Noto Sans JP;
font-weight: 600;
font-style: normal;
}
</style>

---

<h1 class="h1">どんな時に使う？</h1>

動的に型が変わる場合に使う。<br/>
<!--anyでもいいのかもしれないが、anyを使った場合、その変数に対する型チェックが行われなくなるため、<br/>
型ガードなどでチェックする前に、うっかり別の変数や引数などにその変数を指定したり、<br/>
その変数に対するメンバーを参照したりして、予期しないランタイムエラーが起きる可能性がある。<br/>
そこで「unknown 型」を使うことで、型ガードを入れないとほとんどの操作でエラーになるため、うっかりによる事故をある程度軽減することができる。-->

```ts 
declare const maybe: unknown;
// 'maybe' could be a string, object, boolean, undefined, or other types
const aNumber: number = maybe;
//Type 'unknown' is not assignable to type 'number'.
 
if (maybe === true) {
  // TypeScript knows that maybe is a boolean now
  const aBoolean: boolean = maybe;
  // So, it cannot be a string
  const aString: string = maybe;
Type 'boolean' is not assignable to type 'string'.
}
 
if (typeof maybe === "string") {
  // TypeScript knows that maybe is a string
  const aString: string = maybe;
  // So, it cannot be a boolean
  const aBoolean: boolean = maybe;
Type 'string' is not assignable to type 'boolean'.
}
```

<br>
<br>

<style>
.h1 {
font-family: Poppins, Noto Sans JP;
font-weight: 600;
font-style: normal;
}
</style>

---


<h1 class="h1">ちなみに</h1>


```ts 
let p: number | unknown;   // unknown 型になる
let q: number & unknown;   // number 型になる
let m: null | unknown;     // unknown 型になる
let n: null & unknown;     // null 型になる
```

<br>
<br>

<style>
.h1 {
font-family: Poppins, Noto Sans JP;
font-weight: 600;
font-style: normal;
}
</style>

---


<h1 class="h1">never型とは</h1>

値を持たない型。<br/>
never型はあらゆる型に代入可能であるが、never型にはnever型以外は代入できない。

<br>
<br>　

<style>
.h1 {
font-family: Poppins, Noto Sans JP;
font-weight: 600;
font-style: normal;
}
</style>

---


<h1 class="h1">どんな時に使う？</h1>

エラー処理の戻り値の型など、
- 実行される可能性のあるreturn文が存在しないと判断できるとき
- この関数は最後まで到達することはないと判断できるとき

```ts
// 最後まで到達しない関数はnever型の返り値となる
// 必ず通過するthrow文により最後まで到達しない（到達する実行パスが存在しない）
function error(message: string): never {
    throw new Error(message);
}
// 推論される返り値はnever型
// 上で作ったerror関数を返り値‍に指定してるので、必ず通過するthrow文により最後まで到達しない(到達する実行パスが存在しない）
function fail(): never {
    return error("Something failed");
}
// 最後まで到達しない関数はnever型の返り値となる
// → 無限ループに必ず入る場合も throw 文を通る実行パスが無い場合と同様
function infiniteLoop(): never {
    while (true) {
    }
}
```

<style>
.h1 {
font-family: Poppins, Noto Sans JP;
font-weight: 600;
font-style: normal;
}
</style>

---

<h1 class="h1">どんな時に使う？</h1>

switch文の中でneverの出現を頼りに網羅的なチェックをすることができる

```ts
type Shape = Circle | Square;
 
function getArea(shape: Shape) {
  switch (shape.kind) {
    case "circle":
      return Math.PI * shape.radius ** 2;
    case "square":
      return shape.sideLength ** 2;
    default:
      const _exhaustiveCheck: never = shape;
      return _exhaustiveCheck;
  }
}
```


<br>
<br>

<style>
.h1 {
font-family: Poppins, Noto Sans JP;
font-weight: 600;
font-style: normal;
}
</style>

---


<h1 class="h1">どんな時に使う？</h1>

switch文の中でneverの出現を頼りに網羅的なチェックをすることができる

```ts
interface Triangle {
  kind: "triangle";
  sideLength: number;
}
 
type Shape = Circle | Square | Triangle;
 
function getArea(shape: Shape) {
  switch (shape.kind) {
    case "circle":
      return Math.PI * shape.radius ** 2;
    case "square":
      return shape.sideLength ** 2;
    default:
      const _exhaustiveCheck: never = shape;
//Type 'Triangle' is not assignable to type 'never'.
      return _exhaustiveCheck;
  }
}
```

<br>
<br>

<style>
.h1 {
font-family: Poppins, Noto Sans JP;
font-weight: 600;
font-style: normal;
}
</style>

---


<h1 class="h1">Void型と何が違うの？</h1>

- Void型は関数が正常に終了した結果何も返さない時に使う型
- Never型はそもそも関数が正常に終了しない時につかう型


<br>
<br>

<style>
.h1 {
font-family: Poppins, Noto Sans JP;
font-weight: 600;
font-style: normal;
}
</style>

---



<h1 class="h1">おわり</h1>



<br>
<br>

<style>
.h1 {
font-family: Poppins, Noto Sans JP;
font-weight: 600;
font-style: normal;
}
</style>

---


