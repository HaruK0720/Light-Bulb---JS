# 文字列の書き換え

Paizaの「指定位置の文字を置換」問題で、またインデックスの罠にやられました(´;ω;｀)　今回は文字列の書き換えの問題について解説！

<br>

## 問題概要

文字列 `S`、整数 `i`（位置）、文字 `c` が与えられる

`S` の `i`文字目 を `c` に置き換えて出力せよ

入力例:

    ABCDEFGHIJKLMNOPQRSTUVW&XYZ
    16 !

出力例:

    ABCDEFGHIJKLMNO!QRSTUVW&XYZ

<Br>

https://paiza.jp/works/mondai/string_primer/normal_step3

<br><br>

## NGコード：ズレ
```js
const rl  = require('readline').createInterface({input:process.stdin});
const lines = [];


rl.on('line', input => lines.push(input));
rl.on('close',()=>{
    const S = lines[0];
    const [i,c] = lines[1].split(' ');
    
    const result = S.slice(0,Number(i)) + c + S.slice(Number(i)+1);
    
    console.log(result);
});
```

🔻 `i` は 1-based（1文字目が1）なのに、JavaScriptの `.slice()` は 0-based。
つまり「1引く」必要あり！

<br>

## ✅ OKコード：ズレ補正
```js
const index = Number(i) - 1;
const result = S.slice(0, index) + c + S.slice(index + 1);
```
🔧 `.slice()`は [start, end) の半開区間。end は含まないので `index + 1` を使う。

<br>

### ✅ 配列化アプローチ：さらに読みやすく
```js
const chars = S.split('');
chars[index] = c;
console.log(chars.join(''));
```
- `.split('')` → 配列に

- `chars[index] = c` → 置換

- `.join('')` → 再び文字列に

👉 直感的！文字列の書き換えには実はこっちの方が見やすくて安全かも。

<br>

## 💡 技術メモまとめ

- JSのインデックスは 0-based、でも入力が 1-based なら `-1` する
- `.slice(start, end)` の end は含まれない（＝半開区間）
- `.split()` → `.join()` の編集パターンは、柔軟かつ安全


<br><Br><br> [僕の失敗談(´;ω;｀)と解決法🐈](https://paizabeginner.wordpress.com/2025/05/12/paiza%e3%81%a7%e5%9f%ba%e6%9c%ac%e3%83%9e%e3%82%b9%e3%82%bf%e3%83%bc%ef%bc%9a%e6%96%87%e5%ad%97%e5%88%97%e3%81%ae%e6%9b%b8%e3%81%8d%e6%8f%9b%e3%81%88/)
