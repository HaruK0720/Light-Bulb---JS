# 大文字小文字の反転



今日やったのは `A` を `a` にして `pAIZA` を `Paiza` に戻すみたいな割とシンプルな問題。大文字小文字の反転問題について解説！

<br>

## 問題概要

大文字と小文字のアルファベットが混ざった文字列 `S` が与えらる。
`S` の小文字を全て大文字に、大文字を全て小文字にした文字列を出力せよ。
<Br>
入力例：
    
    Paiza

出力例：
    
    pAIZA
<br>

https://paiza.jp/works/mondai/string_primer/normal_step8

<br>

## ✅コード例
```js
const rl = require('readline').createInterface({input:process.stdin});

rl.once('line',(input)=>{
     // 入力された文字列を1文字ずつの配列に変換する
    const text = input.split('');

    // 大文字・小文字を反転した結果を格納する配列
    const flippedCase = [];

    // 文字ごとに処理を行う
    text.forEach(char => {

        // 文字が大文字の場合（toUpperCaseしても変わらない）
        if (char.toUpperCase() === char) {

            // 小文字に変換して追加
            flippedCase.push(char.toLowerCase());
        }

        // 文字が小文字の場合（toLowerCaseしても変わらない）
        else if (char.toLowerCase() === char) {

            // 大文字に変換して追加
            flippedCase.push(char.toUpperCase());
        }
    });

    // 配列を文字列に戻して出力
    console.log(flippedCase.join(''));
})
```
    
- 文字列を配列に変換 `input.split'')`：1文字ずつ処理できるようにする
- 大文字か小文字か判定 ：`char.toUpperCase() === char` などで判定
- 大文字↔小文字変換 ：`toLowerCase()` / `.toUpperCase()` を使って反転
- 出力 `console.log()` で反転後の文字列を表示

<br>

### 🔍 ポイントは「変換前と変換後が一致するかどうかの比較」

例として、`char = “A”` のとき：
```js
char === char.toUpperCase() → true（＝もともと大文字だった）
```
逆に `char = “a”` のとき：
```js
char === char.toUpperCase() → false（＝もともと小文字だった）
```
つまり、

- `char === char.toUpperCase()` が true → 大文字だった

- `char !== char.toUpperCase()` が true → 小文字だった

という「変換しても変わらなかったかどうか」を見て、判別する仕組み。
```js
if (char === c.toUpperCase()) {
    // 変換しても変わらない → 大文字
} else {
    // 変換された → 小文字
}
```

<br>

## 気づきメモ

- `.toUpperCase()` や `.toLowerCase()` は「変換」だけじゃなく、「判定」にも使える！
- `char === char.toUpperCase()` の発想が新鮮だった。

## <br>まとめ

とりあえず変換して、比べてみる！


<br><Br><br>[僕の失敗談(´;ω;｀)と解決法🐈](https://paizabeginner.wordpress.com/about/)
