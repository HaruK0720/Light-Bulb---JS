# reduceの使い方（荷物検査）

今回は、paizaの「荷物検査」の問題に挑戦！

配列の合計値を出すのにループ処理じゃなくて、`reduce` を使ってみることに！

<br>

# 問題概要

- 荷物の個数 N と、重さの基準値 M が与えられる

- 与えられた各荷物の重さを全部足す

- 合計が基準値以下 → "OK"、超えたら "NG"

<br>

入力例:

    5 50
    23
    5
    14
    6
    9

出力例:

    NG

<br>

https://paiza.jp/works/mondai/rank_test_problems_c_0001/rank_test_problems_c_0001__3

<br><br><br>

# ✅OK例：
```js
const rl = require('readline').createInterface({input: process.stdin});
const lines = [];

rl.on('line', (input) => {
    lines.push(input);
});

rl.on('close', () => {
    const [N, M] = lines[0].split(' ').map(Number);
    const weight = lines.slice(1).map(Number);

    const sum = weight.reduce((acc, cur) => acc + cur, 0);

    console.log(sum <= M ? 'OK' : 'NG');
});
```

  
- reduce で 重さの合計 を計算

- 三項演算子 で合計と基準値 M を比較

- M 以下 → "OK" ／ 超える → "NG" を出力

<br><br><br>

# 💡reduce

`reduce` は 配列の要素を 1 つずつ順番に処理して、1 つの値にまとめる ときに使うメソッド!

<br>

## ✅ ざっくり意味

「累積する」 と覚えるといい！
<br>

たとえば配列 [1, 2, 3, 4] の合計を出すとき、

最初に 1 と 2 を足して 3 にする

次に 3 と 3 を足して 6 にする

次に 6 と 4 を足して 10 にする

→ 最後に 10 になる
<br>

これを 自動でやってくれる のが reduce。

<br>

## ✅ 基本構文
```js
const result = array.reduce((accumulator, currentValue) => {
  // 処理
  return 新しい累積値;
}, 初期値);
```

- `accumulator`（累積値）：これまでの計算結果を保持する
- `currentValue`（現在の要素）：今処理している要素
- 初期値：`accumulator` の初期値（必ず設定しよう！）

<br>

## ✅ 例：合計を出す
```js
const arr = [1, 2, 3, 4];

const sum = arr.reduce((acc, cur) => {
  return acc + cur;
}, 0);

console.log(sum); // 10
```
```js
const arr = [1, 2, 3, 4];

const sum = arr.reduce((acc, cur) => acc + cur, 0);

console.log(sum); // 10
```
    
    
- `acc` が累積の結果
-  `cur` が配列の要素
- 初期値が 0 なので、最初は 0 + 1 = 1 から始まる

### ✅ どういう順番で動いているか
```
ステップ1: acc = 0, cur = 1 → acc = 0 + 1 = 1
ステップ2: acc = 1, cur = 2 → acc = 1 + 2 = 3
ステップ3: acc = 3, cur = 3 → acc = 3 + 3 = 6
ステップ4: acc = 6, cur = 4 → acc = 6 + 4 = 10
```

<br>

## ✅ reduce を使うときのコツ

- 初期値を入れ忘れない！
    （初期値が無いと、最初の要素が初期値として使われる → 意図しない動きになることが多い）

- ロジックが複雑になる場合は `for` の方が読みやすいこともある

<br><br><br>

# 📝メモ＆まとめ

- `reduce` は配列の要素を1つの値にまとめる便利メソッド

- `acc`（累積値）に`cur`（現在の値）を順番に足すだけ

- 初期値 を絶対忘れない！

- `Number`に変換しないと数字が繋がるだけだから注意！
- `for` でもできるけど、`reduce` の方がかっこいい（重要）

<br><br><br><br><br>

# 💡おまけ：reduce でできること

## ✅ ① 最大値・最小値
```js
const numbers = [5, 1, 9, 3, 7];

// 最大値
const max = numbers.reduce((acc, cur) => Math.max(acc, cur), -Infinity);
console.log(max); // 9

// 最小値
const min = numbers.reduce((acc, cur) => Math.min(acc, cur), Infinity);
console.log(min); // 1
```
  
- `Math.max` / `Math.min` で累積して比較していく
- 初期値を `-Infinity`（最大値）や `Infinity`（最小値）にするのが安全

<br>

## ✅ ② 配列をオブジェクトに変換
```js
const fruits = ["apple", "banana", "apple", "orange", "banana"];

// 各果物の個数を数える
const count = fruits.reduce((acc, cur) => {
  acc[cur] = (acc[cur] || 0) + 1;
  return acc;
}, {});

console.log(count); // { apple: 2, banana: 2, orange: 1 }
```
- `acc` はオブジェクトとして累積
- 各要素をキーにして、個数を数える

<br>

## ✅ ③ フラット化（2次元配列 → 1次元配列）
```js
const array2D = [[1, 2], [3, 4], [5]];

const flat = array2D.reduce((acc, cur) => acc.concat(cur), []);

console.log(flat); // [1, 2, 3, 4, 5]
```
  
- `concat` で配列をつなげていく
- 初期値は空配列 `[]`

<br>

## ✅ ④ 平均値を求める
```js
const numbers = [1, 2, 3, 4, 5];

const sum = numbers.reduce((acc, cur) => acc + cur, 0);
const avg = sum / numbers.length;

console.log(avg); // 3
```
  
<br>

## ✅ ⑤ 文字列連結
```js
const words = ["Hello", "world", "!"];

const sentence = words.reduce((acc, cur) => acc + " " + cur);

console.log(sentence); // "Hello world !"
```
  

<br>

## ✅ ポイントまとめ

- `reduce` は要素を 1 つずつ累積するから、「まとめて 1 つの値にしたい」 ときに最強
- 配列 → 数値、文字列、オブジェクト、配列 どれでもOK
- 初期値をどうするかが大事（配列なら `[]`、オブジェクトなら `{}` など）


<br><br><br>[僕の失敗談(´;ω;｀)と解決法🐈](https://paizabeginner.wordpress.com/about/)
