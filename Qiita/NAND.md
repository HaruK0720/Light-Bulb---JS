# NAND 演算の基本 !(A & B)

「0と1だけでこんなに奥深い世界があるなんて…！」
Paizaで出会ったNAND（ナンド）演算、正直ナメてた。でもコイツ、実は論理界のチートキャラだった！

問題概要

`0` または `1` の整数 `A` と `B` が与えられ、`A NAND B` を求めるというシンプルなお題。
※ `NAND` = `!(A & B)` のこと。

<br>例）
```
入力: 1 1
出力: 0
```
<br>

https://paiza.jp/works/mondai/logical_operation/logical_operation__basic_step5



## NG例
```js
const [A, B] = input.split(' ');
console.log(!(A & B)); // → true/false（数値じゃない）
```

## <br>OK例
```js
const [A, B] = input.split(' ').map(Number); //.map(Number)はなくてもよい
console.log(Number(!(A & B)));  // NAND = NOT (A AND B)
// → 0 or 1（数値）
```

## <br>まとめ
- `NAND`は「`NOT(AND)`」の略
- 数値変換をする
- `NAND`だけで全論理ゲート作れる → 「万能ゲート」と呼ばれる



<br><br>[🐻僕の失敗談(´;ω;｀)と解決話！🚀🐈](https://paizabeginner.wordpress.com/2025/04/27/paiza%e3%81%a7%e5%9f%ba%e6%9c%ac%e3%83%9e%e3%82%b9%e3%82%bf%e3%83%bcnand-%e6%bc%94%e7%ae%97%e3%81%ae%e5%9f%ba%e6%9c%ac-a-b/)

## <br> おまけ　
`NAND`だけで他の論理演算が作れる！
→ これを「万能ゲート」って言うらしい。

代表的なやつ：

`NOT A` = `A NAND A`

`A AND B` = `(A NAND B)` を `NOT`

`A OR B` = `(A NAND A) NAND (B NAND B)`

`A XOR B = (A NAND B) AND (A OR B)`

<br>

```js
// 論理否定（NOT A）
const notA = Number(!(A & A)); // NOT A = A NAND A


// 論理積（A AND B）
const nand = Number(!(A & B));
const and = Number(!nand); // A AND B = NOT (A NAND B)


// 論理和（A OR B）
const notA_for_or = Number(!(A & A));
const notB_for_or = Number(!(B & B));
const or = Number(!(notA_for_or & notB_for_or)); // A OR B = (A NAND A) NAND (B NAND B)


// 排他的論理和（A XOR B）
const xor = Number(!( !(nand & or) )); // A XOR B = (A NAND B) AND (A OR B)
```
