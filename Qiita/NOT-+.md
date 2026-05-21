# 否定( NOT )の基本 !  (+単項プラス)

「0を1に、1を0に」──めちゃくちゃ単純な話のはずなのに、1回つまづいた…。

## <br>🧩 問題概要

入力が `0` または `1` のとき、論理的に反転して出力する。

- 入力例：`0` → 出力：`1`
- 入力例：`1` → 出力：`0`

<br>

https://paiza.jp/works/mondai/logical_operation/logical_operation__basic_step3

## <br>❌ NGコード
```js
console.log(!A);
```
- `!0` → `true`
- `!1` → `false`

出力が `boolean` になってしまう！数値が欲しいのに！

## <br>✅ OKコード
```js
console.log(+!A);
```
これは `!A` で反転 → `+` で数値化（単項プラス）。

- `+!0` → `+true` → `1`
- `+!1` → `+false` → `0`

## <br>💡 技術ポイントまとめ

- `!A` は「boolean反転」だけど、型が `boolean`
- `+!A` で `boolean` → `number` に変換（`true`→`1`, `false`→`0`）
- `Number(!A)` でもいいけど、`+!A` の方が短くてスマート

<br><br>[僕の失敗談(´;ω;｀)と解決話！🚀](https://paizabeginner.wordpress.com/2025/04/25/paiza%e3%81%a7%e5%9f%ba%e6%9c%ac%e3%83%9e%e3%82%b9%e3%82%bf%e3%83%bc%ef%bc%9a%e5%90%a6%e5%ae%9a-not-%e3%81%ae%e5%9f%ba%e6%9c%ac/)
