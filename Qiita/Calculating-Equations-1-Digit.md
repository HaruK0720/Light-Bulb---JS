# 数式の計算（ 1 桁）

Paizaの「文字列から数式を計算する」問題をやってみたら、数字と演算子が混ざって混乱？！　問題の解説と失敗しそうなところについて書いたよ！

<br>

## 問題概要

与えられるのは、1桁の数字と + – だけで構成された数式の文字列（例：”1+2-3+4“）。
この式をちゃんと計算して数値で出力する

例として、`1-2`, `2+1-7` のような文字列は与えられる可能性があるが、`1+(-2)` や `-4-2+4`, `5+-2` のような文字列は与えられないことが保証されている点に注意。

```
入力例:
1-3-5-6-2-1+9

出力例2:
-7
```
<br>

https://paiza.jp/works/mondai/string_primer/advance_step8

<br><br>
## ✅ 完成コード例

```js
const rl = require('readline').createInterface({ input: process.stdin });

rl.once('line', (input) => {

    // ステップ1: 一文字ずつの配列に
    const chars = Array.from(input);


    // ステップ2: 初期値は最初の数字
    let result = Number(chars[0]);


    // ステップ3: 演算子と数値のセットで処理
    for (let i = 1; i + 1 < chars.length; i += 2) {
        const op = chars[i];
        const num = Number(chars[i + 1]);

        if (op === '+') result += num;
        else if (op === '-') result -= num;
    }

    // ステップ4: 結果を出力
    console.log(result);

    rl.close();
});
```
1: `Array.from(input)` で1文字ずつに分割

2:  最初の数値をresultとして確保

3.`for` でインデックス1から、2つずつ

- 演算子（`+` or `-`）を取得
- 数字を`Number()`で変換して加減算

4: 結果を`console.log(result)`で出力！

<br><br>

## for ループの終了条件の設定ミスによる NG例（バグが起きやすい書き方）

### ❌ NG例1：i <= chars.length

```js
for (let i = 1; i <= chars.length; i += 2) {
    const op = chars[i];

    // ↓ ここで undefined にアクセスする可能性！ 
    const num = Number(chars[i + 1]); 
}
```
❗問題点：

- `chars.length` は「要素数」。
- インデックスは 0 ~ chars.length – 1。

`i <= chars.length` だと、`chars[i + 1]` が範囲外になる可能性　→ `undefined` を `Number()` に渡して `NaN` に！

<br>

### ❌ NG例2：i < chars.length だけど、i + 1 のチェックをしていない

```js
for (let i = 1; i < chars.length; i += 2) {
    const op = chars[i];

    // ↓ ここも念のため注意
    const num = Number(chars[i + 1]); 
}
```
⚠ 注意点：
通常の数式（演算子と数字が交互に並ぶ）では問題ないが、
万が一、入力が “`1+2+`” のように末尾に演算子だけ残った場合、`chars[i+1]` が `undefined` になる。

<br>

### ✅ 安全な OK例（おすすめ）i + 1 < chars.length
```js
for (let i = 1; i + 1 < chars.length; i += 2) {
    
    const op = chars[i];
    const num = Number(chars[i + 1]);
    if (op === '+') result += num;
    if (op === '-') result -= num;
}
```

<Br>

## 気づきメモ

- `i + 1 < chars.length` が地味に超大事
- 最初の数字を初期値にすることで、後は演算子と数字を交互に読むだけでOK！

<br>

### 📘新しく学んだこと　&　まとめ

- `Array.from()` で文字列を1文字ずつ扱えるのは便利！
- `for (i + 1 < length)` の形で「次の値」を安全にチェック
- `Number()`で変換する前に`undefined`対策を考えるクセが大事

<br><br>
 [僕の失敗談と解決話！](https://paizabeginner.wordpress.com/about/)
