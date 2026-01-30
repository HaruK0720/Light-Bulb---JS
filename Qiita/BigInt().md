# JavaScriptで超巨大数を扱う！　Number()で桁落ち？ BigInt()も罠？

Paizaの問題、見た目シンプルだけど地味に落としがあった！。
出力するだけのはずが、`Number()` で数が削れちゃった…。↓

## <br>🔍 問題概要 （「とても大きな数値を出力」）

入力例: 12345678901234567890  
出力例: 12345678901234567890

<br>

https://paiza.jp/works/mondai/data_structure/data_structure__string_step1

## <br>⚠️ NGコード（桁落ちの原因）
```js
const rl = require('readline').createInterface({ input: process.stdin });

rl.on('line', (input) => {
  const n = Number(input);
  console.log(n);
});
```
出力結果:
```
12345678901234567000 // ←あれ？
```
JavaScriptのNumber型（IEEE 754 double）は約16桁までしか正確に扱えない。

## <br>✅ 正しいコード：文字列で扱う
```js
rl.on('line', (input) => {
  console.log(input);
});
```
文字列のまま出力すれば、精度は失われない。今回は「そのまま出す」だけなので、一切変換しないのが正解！

## <br>❌ BigIntも要注意
```js
const big = BigInt(input);
console.log(big); // 出力: 12345678901234567890n ←不正解！
```
`BigInt`は便利だけど、出力時に `n` がつくので、表示するときは文字列化する必要がある！

```js
const big = BigInt(input);
console.log(String(big)); // 出力: 12345678901234567890 ←正解！
```


## <br>✅ 要点まとめ
- `Number()`は桁落ちする。特に15桁超えは注意。
- 出力だけなら、文字列のまま扱うのがベスト。
- `BigInt`は演算向き。出力用途には向かない（`n`がつくため）。

【注意点】
`BigInt` は 少数（小数点）を扱えない。
`Number` 型と直接混ぜて使えない。`BigInt` 同士でしか演算できない。

<br><br>[僕の失敗談(´;ω;｀)と解決話！🚀](https://paizabeginner.wordpress.com/2025/04/18/paiza%e3%81%a7%e5%9f%ba%e6%9c%ac%e3%83%9e%e3%82%b9%e3%82%bf%e3%83%bc%ef%bc%9a%e8%b6%85%e3%83%87%e3%82%ab%e3%81%84%e6%95%b0%e3%81%af%e3%80%8cbigint%e3%80%8d%e3%81%a7%e4%b9%97%e3%82%8a%e3%81%93%e3%81%aa/)

