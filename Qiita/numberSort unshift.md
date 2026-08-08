# 約数の列挙



今日も前回に続いて約数の問題をループ処理を使って解いていく！

前回の平方根の考え方を応用しようとしたら、ちょっとつまづいたけど、最終的にはうまくいってよかった🚀

<br><br>

## 問題概要

- 整数 N が与えられる。
- N の約数を小さい方から順に改行区切りで出力せよ。

<br>

入力例：

    10

出力例：

    1
    2
    5
    10

<br>

https://paiza.jp/works/mondai/loop_problems2/loop_problems2__divsor_print

<br><br><br>

## ✅ OK例：
```js
const rl = require('readline').createInterface({input:process.stdin});


rl.once('line', (input) => {
    const N = Number(input);
    
    const divisor = [];
    for (let i = 1; i <= N; i++){
        if (N % i === 0){
           divisor.push(i); 
        }
    }
    
    divisor.forEach(num => console.log(num));
    
    rl.close();
});
```
- 1からNまでを調べる
- 約数を見つけたら配列に格納
- 出力する

1から調べていっているので、勝手に昇順で配列に格納されて、そのまま出力される。

<br><br><br>

## 💡前回の学びを応用してみよう！

前回、約数を見つけるのに、

ループを回すのは、N の「平方根」までで十分であり、

そうすると計算量を大幅に減らせる場合もあると学んだ！

<br>

### ❌ NG例
```js
const rl = require('readline').createInterface({input:process.stdin});


rl.once('line', (input) => {
    const N = Number(input);
    
    const divisor = [];
    for (let i = 1; i <= Math.sqrt(N); i++){
        if (N % i === 0){
           divisor.push(i); 
           divisor.push(N / i);
        }
    }
    
    [...new Set(divisor)].sort().forEach(num => console.log(num));
    
    rl.close();
});
```

❌問題点
`sort()` はデフォルトで文字列として並べるので、
例えば、2の前に10が出力されてしまう。

<br>

※このコードの意図（読み飛ばしてください(´;ω;｀)）

Setを使えば重複を防げるから、一担 Set に入れて、スプレッド構文で配列に戻して、昇順に並び替えて出力すればいいという考え。

ちなみに、そのときは、重複する約数を2回pushしないようにするように条件分岐を書くより、setで処理した方が楽そうだと思った。

<br><br>

### ✅ 方法①：数値として正しく .sort() する
```js
[...new Set(divisor)]
  .sort((a, b) => a - b)  // 数値の昇順で並び替え
  .forEach(num => console.log(num));
```

<br>

### ✅ 方法②：そもそも順番を気にして最初から前後に分けておく
```js
const small = [];
const large = [];

for (let i = 1; i <= Math.sqrt(N); i++) {
  if (N % i === 0) {
    small.push(i);
    if (i !== N / i) large.unshift(N / i); // 重複防止
  }
}

[...small, ...large].forEach(num => console.log(num));
```
→この方法だと `sort()` しなくても 最初から昇順になる

💡ポイント
- `（i !== N / i）` で平方根の重複を避ける。
- `.unshift()` で配列の先頭に要素を追加することで、後半の約数を順番通りに並べる。
- スプレッド構文を使って、配列同士をつなげて出力。

<br>

※補足

例）N = 10

- 1、2、5、10 が約数である　
- [1 と 10]、 [2 と 5] でペアとした時
    - 1と2が小さい約数
    - 5と10が大きい約数

ペアで考えてみると、大きい約数は配列の「前から」いれないと昇順にならないとわかる。

<br><br>

## 📝 気づきメモ & まとめ

- `.sort((a, b) => a - b)` ← 数値ソートの基本！
- `.unshift()` を使うと先頭に要素を追加できる。
- ループは平方根までで十分
    - 約数は 小さい × 大きい のペアで出ることを意識すると効率的。
- スプレッド構文で配列を結合！


<br><br><br>[僕の失敗談(´;ω;｀)と解決法🐈]()

