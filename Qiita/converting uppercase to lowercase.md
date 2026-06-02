# 大文字から小文字への変換

大文字小文字が混ざった文字列、「これ全部小文字にするやつどう書くの!?」ってなったけど、便利なメソッドがあった！

<br>

## 問題概要

大文字と小文字のアルファベットが混ざった文字列 `S` が与えられるので、`S` を全て小文字にした文字列を出力せよ。

入力例：

    PAIZA

出力例：

    paiza

<br>
https://paiza.jp/works/mondai/string_primer/normal_step6

<br><br>

## ✅コード例
```js
const rl = require('readline').createInterface({input:process.stdin});

rl.once('line',(input)=>{

    let lowerCaseText = input.toLowerCase();
    console.log(lowerCaseText); 
    
    rl.close();
});
```
入力を `.toLowerCase()` で小文字に変換して `console.log` で出力！

<br><br>

## .toLowerCase()とは？

`.toLowerCase()` は、JavaScript において 文字列をすべて小文字に変換するためのメソッド。

### 🔧 基本構文
```js
let str = "HeLLo";
let lower = str.toLowerCase(); // "hello"
```
<Br>

### 📌 特徴とポイント

![スクリーンショット 2025-05-13 122602.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4018208/d42c118b-8c54-49aa-92d3-a6e70a9bc3dd.png)

<br>

###📚 使用例
```js
console.log("JAVASCRIPT".toLowerCase()); // "javascript"
console.log("PaIZa123!".toLowerCase());   // "paiza123!"
```
<Br>

### ⚠ 注意点

- 数字・記号・空白などは影響を受けない
```js
"123!@#ABC".toLowerCase() // → "123!@#abc"
```

- undefined や null に使おうとするとエラーになる。文字列型であることを確認して使う。

<br>

### 🔍 実践での活用シーン例

ユーザーの入力を 大文字小文字を区別せずに比較したいとき：
```js
if (userInput.toLowerCase() === "yes") {
    // OK
}
```
<Br><br>


## 💡気づきメモ

- .toLowerCase()は非破壊的（元の文字列を変えない）
- アルファベットだけ小文字化。数字や記号、日本語はそのまま
- 判定処理にも活用できる！

<br>

## 新しく学んだこと 

- `String.toLowerCase()` → 小文字変換の王道
- `typeof` で文字列チェックしてから使うと安心
- 入力に応じた柔軟な前処理の大切さ
- `.toUpperCase()`：こっちは大文字に変換。処理の逆方向。

<br>

## まとめ

文字列の大小文字を処理するのに `.toLowerCase()` は超定番！

<Br><br><br>[僕の失敗談(´;ω;｀)と解決法🐈](https://paizabeginner.wordpress.com/about/)
