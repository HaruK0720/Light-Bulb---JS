# 文字列の挿入



文字列の一部を追加したりする操作って、意外と最初はピンとこない…。今回は文字列の挿入問題について解説する！

<br><br>

## 🔍 問題概要

文字列 `S`, `T` と整数 `N` が与えられるので、`S` の `N`文字目の「後ろ」に `T` を挿入して出力せよ。

入力例：

    abcde
    fghij
    5

出力例：

    abcdefghij
<br>

https://paiza.jp/works/mondai/string_primer/normal_step2

<br><br>

## 🛠 解き方：sliceで分割＆合体
```js
const rl = require('readline').createInterface({ input: process.stdin });
const lines = [];

rl.on('line', line => lines.push(line));
rl.on('close', () => {

    const S = lines[0];
    const T = lines[1];
    const N = Number(lines[2]);


    // S の N文字目の後ろ → index N で分割（0-indexed）
    const result = S.slice(0, N) + T + S.slice(N);

    console.log(result);
});
```
- `N` は 1-based（1 文字目が 1）
- `slice` は 0-based（1 文字目が index 0）
    この一行で「前半 + `T` + 後半」が完成！ `slice` は本当に便利。

<br><br><br>

## 💡他のコード例

「他のやり方」や「新しいメソッド」に挑戦するのも良い練習になるので、以下にいくつかの別解を紹介する！
<br>

### 方法①：配列に変換して splice() を使う

```js
const rl = require('readline').createInterface({ input: process.stdin });
const lines = [];

rl.on('line', line => lines.push(line));
rl.on('close', () => {
    const S = lines[0];
    const T = lines[1];
    const N = Number(lines[2]);



    const arr = S.split('');     // 文字列を配列に分解
    arr.splice(N, 0, T);         // N 番目の位置に T を挿入
    console.log(arr.join(''));   // 配列を文字列に戻す
});
```
<br>

### 方法②：substring() を使う
```js
const result = S.substring(0, N) + T + S.substring(N);
```
※ `slice()` と似てるが、引数が負のときの挙動が違う。

<br>

### 方法③：replace() + 正規表現（ちょっと強引）
```js
const result = S.replace(new RegExp(`^(.{${N}})`), `$1${T}`);
```
- `^(.{N})` は先頭から `N` 文字をキャプチャ
- `$1${T}` でその直後に `T` を挿入

<br>

### 方法④：スプレッド構文を使って splice()
```js
const arr = [...S]; // スプレッド構文で配列化
arr.splice(N, 0, T);
console.log(arr.join(''));
```

<br><br>

## ✅ 気づきメモ

- `slice()`で切ってつなぐのが一番直感的でシンプル！
- `splice()`は配列操作だから、ちょっと大げさ
- `substring()`でも同じことはできるけど、負の数の扱いがちょっと違うので注意
- `replace()`＋正規表現でもゴリ押しできるけど、読みづらい


## <br> 新しく学んだこと

- `slice()` と `substring()` の違い：負の数の扱いに注意
- `splice()` は配列にしか使えない

<br>

## まとめ

ちょっとした操作でも、いろんなやり方があるのが面白いところ！
これからも、「他のやり方」や「新しいメソッド」に挑戦したい！

<br><br><br>[僕の失敗談(´;ω;｀)と解決法🐈](https://paizabeginner.wordpress.com/about/)
