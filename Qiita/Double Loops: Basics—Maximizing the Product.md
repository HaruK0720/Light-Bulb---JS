# 二重ループ：基本編　積の最大




今日は多重ループの範囲で、配列Aと配列Bの要素をかけたときの最大値を求める問題に挑戦！

それぞれの配列の最大値をとって掛ければ簡単に解決！と思ったけど…。違ったみたい(´;ω;｀)

<br>

## 問題概要

- 配列 A と B についての情報が与えられる

- (A の 1 つの要素) × (B の 1 つの要素) の最大値を求めよ

<b4r>

入力例:

    10 10
    85 -46 93 44 -40 -75 -75 -18 -54 95
    1 95 -92 -90 32 -25 36 55 22 86

出力例:

    902

<br>

https://paiza.jp/works/mondai/double_roop_problems/double_roop_problems__multi_max

<br><br><br>


## ❌ NG例：「最大値×最大値」で間違えたコード
```js
const rl = require('readline').createInterface({input:process.stdin});

const lines = [];

rl.on('line', (input) => {
    lines.push(input);
});



rl.on('close', () => {
    const [N, K] = lines[0].split(' ').map(Number);
    const arrA = lines[1].split(' ').map(Number);
    const arrB = lines[2].split(' ').map(Number);
    
    const maxA = Math.max(...arrA);
    const maxB = Math.max(...arrB);
    
    console.log(maxA * maxB);
});
```

<br>

## ❓ なぜ maxA * maxB じゃダメなときがある？

### ✅ 例を見てみる：

- arrA = [-10, -5];
- arrB = [-20, -3];

最大値は：

- maxA = -5
- maxB = -3

maxA * maxB = (-5) * (-3) = 15

<br>

でも…

💡-10 * -20 = 200 ← こっちの方がでかい！！

<br>

❗ 結論：

単に「最大値」を取るだけでは不十分。
なぜなら、負の数 × 負の数 = 正の数で、しかも大きくなり得るから！


<br>

### ❓ じゃあ、絶対値で見てみるのは？

一見よさそうだけど…

- arrA = [-1000, 2]
- arrB = [-1000, 2]

最大の絶対値は 1000 → 1000 * 1000 = 1,000,000

<br>

でも…
その 絶対値 をとった数が同じ符号同士だった場合のみ有効で、異なる符号だった場合、

本来は、
1000 * -1000 = -1,000,000 なのに…。となってしまう。
<br>

→ 絶対値の最大同士を掛けるのは 得策ではない。

<br><br>

## ✅ OK例：すべての組み合わせを試す安全な方法
```js
let max = -Infinity;

for (let a of arrA) {
  for (let b of arrB) {
    max = Math.max(max, a * b);
  }
}

console.log(max);
```
初期値を 0 にしちゃうと、すべての積が負だったときに正しい結果が出ない！
→ だから `-Infinity` を使うのが安全。

<br><br>

## 📝メモ

- 負の数も含める場合、配列Aの最大値 ✖️ 配列Bの最大値 が 最大値 になるとは限らない。
- 絶対値がでかくても、符号の組み合わせ次第でマイナスになる
- 配列×配列の全通りを調べる2重ループが安定かも
- `-Infinity` を初期値にする → どんな数と比べても常に意図した比較ができる

<br>

## まとめ

計算量を減らしたり、スマートなコードにするために、メソッドを駆使してみようと思ったけど、結局、基本の多重ループが安定だった。


<br><br><br>[僕の失敗談(´;ω;｀)と解決法🐈](https://paizabeginner.wordpress.com/2025/06/15/paiza%e3%81%a7%e5%9f%ba%e6%9c%ac%e3%83%9e%e3%82%b9%e3%82%bf%e3%83%bc%ef%bc%9a%e4%ba%8c%e9%87%8d%e3%83%ab%e3%83%bc%e3%83%97%ef%bc%9a%e5%9f%ba%e6%9c%ac%e7%b7%a8%e3%80%80%e7%a9%8d%e3%81%ae%e6%9c%80/)
