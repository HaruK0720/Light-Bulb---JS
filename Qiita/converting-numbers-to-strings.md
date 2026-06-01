# 数値から文字列への変換

数値 [N] って書いたらエラーがでた。数値ってインデックス取得できないんだね…。

<br>

## 問題概要

2つの数値 `X`, `Y` と、1から始まる位置 `N` が与えられます。`X + Y` の結果の、
`N`文字目の数字を出力する問題.



入力例：

    18471
    -1727
    5

出力例：

    4

条件：
・ -10^12 ≦ X , Y ≦ 10^12
・ 0 ≦ X + Y
・ X + Y の計算結果の桁数は N 以上 13 未満
<br>

https://paiza.jp/works/mondai/string_primer/normal_step5

<br>

## ❌NGコード
```js
const rl = require('readline').createInterface({input:process.stdin});
const lines = [];

rl.on('line',input => lines.push(input));
rl.on('close',()=>{

    const [X,Y,N] = lines.map(Number)
    result = (X + Y);
    console.log(result[N])

});
```
❌ 問題点
数値は配列や文字列じゃないのでインデックスアクセスできない！
→ 文字列化してからインデックスで取り出す必要がある。

<br>

## ✅OKコード
```js
const [X, Y, N] = lines.map(Number);
const sumStr = String(X + Y); // 数値を文字列に変換
console.log(sumStr[N - 1]);   // Nは1-indexなので-1する
```
- `String()`で文字列化
- `N - 1` で0-basedに変換（地味に忘れがち）

## <br><br>✅絶対値バージョン（保険）
```js
const [X, Y, N] = lines.map(Number);
const sumStr = Math.abs(X + Y).toString();
console.log(sumStr[N - 1] ?? '');
```
- 負の数でも安心！`Math.abs()`で符号除去

- `?? ''` で足りない桁を空文字にしておく保険（例：`N` が大きすぎても安心）

<br><br>

## 新しく学んだこと

- 数値[N] は使えない → 文字列化してからインデックス参照

- `Math.abs()` と `.toString()`の合わせ技で符号無視処理。

- 数値→文字列→インデックス参照の流れ。

<Br><br><br>[僕の失敗談(´;ω;｀)と解決法🐈](https://paizabeginner.wordpress.com/2025/05/13/paiza%e3%81%a7%e5%9f%ba%e6%9c%ac%e3%83%9e%e3%82%b9%e3%82%bf%e3%83%bc%ef%bc%9a%e6%95%b0%e5%80%a4%e3%81%8b%e3%82%89%e6%96%87%e5%ad%97%e5%88%97%e3%81%b8%e3%81%ae%e5%a4%89%e6%8f%9b/)
