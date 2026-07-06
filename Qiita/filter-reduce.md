# 偶数・奇数カウント【filterとreduceで攻略】


今回は Paiza の問題集条件分岐メニューの「偶数と奇数の個数をカウントする」問題に挑戦！
<br><br>

## 🔍 問題概要

長さ `N` の数列 `A` が与えられる。その中に含まれる 偶数の数と奇数の数をカウントして、「偶数 奇数」の順で出力せよ、という内容。
<Br>

入力例：

    5
    1 2 3 4 5

出力例：

    2 3
<Br>

https://paiza.jp/works/mondai/conditions_branch/conditions_branch__mod_step3

<Br><br><br>

## ✅コード例：
```js
const rl = require('readline').createInterface({input:process.stdin});

const lines = [];


rl.on('line',(input) => {
    lines.push(input);
});


rl.on('close', () => {
    const N = Number(lines[0]);
    const arrA = lines[1].split(' ').map(Number);
    
    let odd = 0;
    let even = 0;
    
    arrA.forEach(num => {
        if(num % 2 === 0){
            even++;
        }else{
            odd++;
        }
    })
    
    console.log(`${even} ${odd}`);
    
});
```
これは王道。問題は解けるけど、「短い」コードも試してみたくなった！

<br><br><br>

## ✨ 解法① filter で書くと？
```js
const evenCount = arrA.filter(n => n % 2 === 0).length;
const oddCount = arrA.filter(n => n % 2 !== 0).length;
```
`filter` → 条件に一致する要素だけ抽出 → `length` で数える
シンプルで読みやすくて超便利！

<Br><br>

## ✨ 解法② reduce で1回ループ
```js
const [even, odd] = arrA.reduce(
    ([e, o], n) => n % 2 === 0 ? [e + 1, o] : [e, o + 1],
    [0, 0]
);
```
`reduce` を使えば 1回のループで偶数奇数を同時に集計できる。慣れるとスッキリ書けて超スマート！

<Br><br><Br>

## 📝 気づきメモ
- filter は 使い所を知ると超便利。条件抽出＋個数カウント。
- `reduce` は 慣れるまで難しいけど1回で処理したいときに便利。
- `for` 文以外の「選択肢」を持っておくとコードが変わる！

<br>

### 🆕 新しく学んだことまとめ

- =n % 2 === 0`で偶数、`!== 0` で奇数。
- `filter().length` で該当数カウント。
- `reduce(([a,b], x) => 条件 ? [a+1, b] : [a, b+1], [0,0])` の書き方。
- `=` と `===` の違いは致命的！（特に`if`文）

## ✅ まとめ

偶奇のカウント、やってみるとシンプルだけど、`filter` や `reduce` の練習になった！

<br><br><br><br><br>

# 💡おまけ①②③
## ①reduce

`reduce` は、配列のすべての要素に対して「累積的な処理」を行いたいときに使う高階関数。配列の合計、カウント、グループ分けなど、さまざまな集計に使える🚀

### ✅ 基本構文
```js
array.reduce((累積変数, 現在の値) => {
    return 新しい累積値;
}, 初期値);
```
<Br>

### ✅ よくあるパターン：合計を求める
```js
const nums = [1, 2, 3, 4, 5];
const sum = nums.reduce((acc, cur) => acc + cur, 0);
console.log(sum); // 15
```
- `acc` : 累積値（ accumulator ）
- `cur` : 現在の要素 ( currentValue )
- `0` : 初期値（`acc`に最初に入る値）

<br>

### ✅ 偶数・奇数カウントの例
```js
const nums = [1, 2, 3, 4, 5];
const [even, odd] = nums.reduce(
    ([e, o], x) => x % 2 === 0 ? [e + 1, o] : [e, o + 1],
    [0, 0]
);
console.log(even, odd); // 2 3
```
- `([e, o], x)` : 累積値を配列で管理
- 初期値 : `[0, 0]` : 偶数カウント0、奇数カウント0 からスタート

<br><br><br>

## ②コード例：超短く
```js
require('readline').createInterface({ input: process.stdin }).on('close', () => {
    const [n, nums] = require('fs').readFileSync('/dev/stdin', 'utf8').trim().split('\n');
    const [even, odd] = nums.split(' ').map(Number).reduce(
        ([e, o], x) => x % 2 === 0 ? [e + 1, o] : [e, o + 1],
        [0, 0]
    );
    console.log(even, odd);
});
```
💡 特徴：

- 一行目で全体を読み込んで、変数展開。
- `reduce` で偶数・奇数カウントを一括処理。
- かなり短くできるけど、読みにくくなるかも。

<br><br>

## ③コード例：関数化して整理
```js
const countEvenOdd = (arr) =>
    arr.reduce(([even, odd], x) => x % 2 === 0 ? [even + 1, odd] : [even, odd + 1], [0, 0]);


const rl = require('readline').createInterface({ input: process.stdin });
const lines = [];

rl.on('line', line => lines.push(line));
rl.on('close', () => {
    const A = lines[1].split(' ').map(Number);
    const [even, odd] = countEvenOdd(A);
    console.log(even, odd);
});
```
💡 特徴：

- `countEvenOdd` という関数にロジックを切り出し。
- 可読性が良く、再利用も可能。
- 本番コードや長めの処理には関数化が便利。

<br><br><br>[僕の失敗談(´;ω;｀)と解決法🐈](https://paizabeginner.wordpress.com/about/)
