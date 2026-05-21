# 半加算器

Paizaの問題解いてたら、足し算をゴリ押しするより論理演算使ったほうがカッコいいじゃんって気づきました。

## <br>📝 問題概要

`0` か `1` の整数 `A` , `B` が与えられる。

`A + B` の2進表記で

下から2桁目 → `C`（Carry：繰り上げ）

下から1桁目 → `S`（Sum：和）

を出力せよ！

例:
```
入力: 
1 1

出力: 
1 0
```
<br>

https://paiza.jp/works/mondai/logical_operation/logical_operation__basic_step8



## <br>例１:普通に足し算
```js
const sum = A + B;
const S = sum % 2;
const C = Math.floor(sum / 2);
console.log(C, S);
```
- `sum = A + B` として普通に足し算する
- `S`は 1の位 を `sum % 2` で求める
- `C`は 繰り上がりを `Math.floor(sum / 2)` で求める

たしかに動くけど、なんか...スマートさに欠ける！

## <br>✅例２：論理演算
```js
const C = A & B; // AND: 両方1なら1
const S = A ^ B; // XOR: 違うときだけ1
console.log(C, S);
```
- `&`（AND） は 「両方が1なら1」 → 繰り上がり（Carry）が発生する条件
- `^`（XOR） は 「どちらか一方が1なら1」 → その桁の合計（Sum）の値





## <br>✍️メモ　まとめ

- `&`（AND）は両方1なら1 → Cにぴったり。
- `^`（XOR）はどちらか一方だけ1なら1 → Sにぴったり。


これが噂の「半加算器」か…!

<br>[失敗談(´;ω;｀)と解決法🐈](https://paizabeginner.wordpress.com/2025/04/30/paiza%e3%81%a7%e5%9f%ba%e6%9c%ac%e3%83%9e%e3%82%b9%e3%82%bf%e3%83%bc%ef%bc%9a%e5%8d%8a%e5%8a%a0%e7%ae%97%e5%99%a8/)
