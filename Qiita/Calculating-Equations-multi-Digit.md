# 数式の計算（多桁）

一桁だと動いたコードが、多桁になった瞬間に崩壊。やっぱり文字列処理、奥深い！

<br>

## 🧪 問題概要

文字列で渡される数式（演算子は `+` と `-` のみ）を計算して、結果を出力せよ。


入力例:
```
781781+272-178781+3919-1737389
```
出力例:
```
-1130198
```
<br>

https://paiza.jp/works/mondai/string_primer/advance_step9

<br>

## 💥 NGコード例
```js
const chars = Array.from(input); // 一文字ずつバラされる
```
こうすると、例 `"781"` が `["7", "8", "1"]` にバラバラ…。
前回の一桁問題と同じようにやって失敗(´;ω;｀)

<br><br>

## ✅ OKコード（正規表現で意味ごと抽出）
```js
const numbers = input.match(/\d+/g).map(Number);
const operators = input.match(/[+-]/g);

let result = numbers[0];
for (let i = 0; i < operators.length; i++) {
  result = operators[i] === "+" ? result + numbers[i + 1] : result - numbers[i + 1];
}
```

### 🔍 解説

- `\d+` ：連続する数字 → 多桁でも1つの塊に
- `[+-]` ：`+` か `-` のどちらか → 記号だけ抽出
- `.match()` ：文字列を「意味単位」で切り分けられる超便利メソッド！
- `g` ：global（全体） → 該当するすべてを対象に抽出！


<br><br>

## ☝️ 技術ポイントまとめ

- 数字と記号をロジック的に分離するには「正規表現 ＋ `match()`」をつかう
- 特に多桁対応では `\d+` が便利
- `split()` や `Array.from()` では構造を失うリスクあり

<br><br>
[僕の失敗談と解決話！](https://paizabeginner.wordpress.com/2025/05/08/paiza%e3%81%a7%e5%9f%ba%e6%9c%ac%e3%83%9e%e3%82%b9%e3%82%bf%e3%83%bc-%e6%95%b0%e5%bc%8f%e3%81%ae%e8%a8%88%e7%ae%97%ef%bc%88%e5%a4%9a%e6%a1%81%ef%bc%89/)
