# 文字列の反転　reverse()



文字列を反転するだけのシンプルな問題。やってみると意外といろんなやり方があった！

<br>

## 問題概要

文字列 `S` が与えられるので、 `S` の前後を反転させた文字列を出力せよ。
<br>
入力例：

    paizaazzap

出力例：

    pazzaaziap

<br>

https://paiza.jp/works/mondai/string_primer/normal_step10

<br>

## ✅コード例：reverse()
```js
// 入力受け取り
const rl = require('readline').createInterface({ input: process.stdin });

rl.once('line', (input) => {

    // ① split('') で1文字ずつの配列に変換 → ['a','b','c','d','e']
    // ② reverse() で順番を反転 → ['e','d','c','b','a']
    // ③ join('') で文字列に戻す → "edcba"

    const reversed = input.split('').reverse().join('');

    // 出力
    console.log(reversed);

    // 入力終了
    rl.close();
});
```

<br>

## 🔁 for文を使って文字列を反転する方法
```js
const rl = require('readline').createInterface({ input: process.stdin });

rl.once('line', input => {
    let reversed = [];

    // 後ろから前に向かって1文字ずつ push
    for (let i = input.length - 1; i >= 0; i--) {
        reversed.push(input[i]);
    }

    // 配列を文字列に変換して出力
    console.log(reversed.join(''));
});
```
✅ 補足ポイント

- `input.length – 1` からスタートして `i >= 0` までループ。
- `.push(input[i])` で逆順に格納。
- 最後に `join'')` で文字列として出力。

`split().reverse().join()` に頼らず、自分でアルゴリズムを制御！

<br>

## 🔁 文字列だけで反転する方法
```js
const rl = require('readline').createInterface({ input: process.stdin });

rl.once('line', input => {
    let reversed = '';

    // 文字列を後ろから1文字ずつ先頭に追加していく
    for (let i = input.length - 1; i >= 0; i--) {

        // 配列ではなく文字列に直接追加
        reversed += input[i]; 
    }

    console.log(reversed);
});
```
✅ ポイント解説

- `let reversed = ''` として空の文字列を初期化。
- `reversed += input[i];` によって、1文字ずつ文字列の末尾に追加。
- 配列 + `join()` を使ってないので、コードが少しシンプル。

<br><br>

## 気づきメモ

- `reverse()` は配列専用。文字列には使えない！
- `join('')` を忘れるとカンマ付きで出力されてしまう…

- 反転方法は3パターン：`split+reverse+join`、`for`文で配列に`push`、文字列に`+=`

## <br>まとめ

最初は簡単そうに見える問題も、実際にコードを書くとたくさんの気づきがあった！Paizaの問題は基礎力アップに最適なので、コツコツ解いていきたい！


<br><br><br>[僕の失敗談(´;ω;｀)と解決法🐈](https://paizabeginner.wordpress.com/about/)
