# 終了判定 2 と while　　おまけ:対数


今回もpaizaの条件分岐の問題を解いたけど、久しぶりにwhileを使ったコードを書いた！
あと、おまけで対数についてまとめてみたから見てみてね！

<br><br>

## 問題概要

2つの整数 `N`, `K` が与えられ、`N` を 2 倍していって `K` 以上になるまでの操作回数 M を求める。
<br>
入力例：

    2 18

出力例：

    4
<br>

https://paiza.jp/works/mondai/conditions_branch/conditions_branch__complex_step5

<br><br><br>

## ✅ OK例（while版）
```js
const rl = require('readline').createInterface({ input: process.stdin });

rl.once('line', (input) => {
    const [N, K] = input.split(' ').map(Number);
    let current = N;  // 現在のNの値
    let count = 0;    // 操作回数（M）

    // NがK以上になるまで、2倍を繰り返す
    while (current < K) {
        current *= 2;
        count++;
    }

    console.log(count);  // 最終的な操作回数Mを出力

    rl.close();
});
```
`current < K` の間は 2倍 し続け、カウントは `K` に到達した時点でストップ！

<br><br>

### ❌ NG例
```js
let count = 0;
while (N <= K) {
    N *= 2;
    count++;
}
```
`N <= K` だと、`N === K` のときも、もう1回ループしてしまう。
つまり「ちょうど `K` のとき」にも2倍されて1回余計にカウントされる。

<br><br>

## ✅他パターン：for
```js
const rl = require('readline').createInterface({ input: process.stdin });

rl.once('line', (input) => {
    const arr = input.split(' ').map(Number); 

    let N = arr[0];
    const K = arr[1];

    // 回数カウントは1から開始（1回目の操作から）
    for (let i = 1; ; i++) {
        N *= 2; // Nを2倍

        if (N >= K) { // K以上になったら回数出力
            console.log(i);
            break; // ループ終了
        }
    }

    rl.close(); 
});
```
- `for (let i = 1; ; i++)` で無限ループしつつ、操作回数をカウント。
- `N` を 2倍 したあと `K` 以上かチェック。
- `K` 以上になった時点で `console.log(i)` し、`break` で終了。

<br><br>

## 📝気づきメモ
- 無限ループ ＋ `break` でもいけるけど、`while`文での明示的な条件設定の方が直感的で安全かも。
- `while`ループでの条件設計力：何を条件にしてどこで止めるか
- 初期値と境界条件の扱いの大切さ（NとKが等しい時など）

<br>

## 📒 まとめ

最初は「ただ倍にするだけでしょ」と思ってたけど、意外に論理的な考え方が試されて面白かった！


<br><Br><br>[僕の失敗談(´;ω;｀)と解決法🐈](https://paizabeginner.wordpress.com/2025/05/31/paiza%e3%81%a7%e5%9f%ba%e6%9c%ac%e3%83%9e%e3%82%b9%e3%82%bf%e3%83%bc%ef%bc%9a%e7%b5%82%e4%ba%86%e5%88%a4%e5%ae%9a-2-%e3%81%a8-while%e3%80%80%e3%80%80-%e3%81%8a%e3%81%be%e3%81%91%e5%af%be%e6%95%b0/)


<br><br><br><br><br>

# 💡おまけ：対数（log）
```js
const rl = require('readline').createInterface({ input: process.stdin });

rl.once('line', (input) => {
    const [N, K] = input.split(' ').map(Number); 

    const M = Math.ceil(Math.log2(K / N)); 
    console.log(M); 

    rl.close(); 
});
```
<br>

## 💡Math.ceil(Math.log2(K / N)) を分かりやすく

### ✅ ステップ1：「2倍していく」とはどういうこと？

たとえば、はじめの数が `N = 2` だったとする。
そして `K = 18` を超えるまで、どんどん 2倍 する。
```
1回目 → 2 × 2 = 4  
2回目 → 4 × 2 = 8  
3回目 → 8 × 2 = 16  
4回目 → 16 × 2 = 32（ここで18を超えた！）
```
👉 このとき、4回で18を超えた。

<br><br>

## ✅ ステップ2：「じゃあ、何回2倍したらいいかを早く計算できないかな？」

毎回2倍して調べるのはちょっと大変…。

そこで登場するのが「log（対数:logarithm）」という考え！

対数とは、ある数を何乗すると指定の数になるかを表す指数のこと。

<br><br>

## ✅ ステップ3：log2ってなに？

「`log2(x)`」は、こう考える👇

<br>

「2を何回かけたら x になる？」
<br>

たとえば：

- `log2(8)` → 答えは 3（なぜなら 2×2×2 = 8）
- `log2(32)` → 答えは 5（2 を 5 回かけると 32）

<br><br>

## ✅ ステップ4：「K / N」はなぜ出てくる？

※ K / N = K ÷ N

さっきの例で `K = 18`, `N = 2` だったよね。
<br>
「N を 2倍して、いつ K を超えるか？」
<br>

ってことは、`K` を `N` で割って「何倍すればいいか」を先に調べればいいんだ！
<br>

```
K / N = 18 / 2 = 9
```
じゃあ、「2を何回かけたら9を超えるのか？」と考える。
```
log2(9) ≒ 3.17（3回じゃ足りない、4回は必要）
```

<br><br>

## ✅ ステップ5：Math.ceil() は「切り上げ」

`Math.ceil(3.17)` → 4 にする
    （小数点があったら、1つ上の整数にする）

なぜなら、3回じゃ足りないから！

<br><br>

## ✅ 🔁 全体をまとめて読むと…
```js
Math.ceil(Math.log2(K / N))
```
はこういう意味👇
<br>
「`N` を 2倍 して `K` を超えるには、何回やればいい？
その回数をちゃんと整数に切り上げて出してね！」

<br><br>

## ✅ まとめ
- `log2(x)`　→　2 を何回かけたら `x` になる？
- `K / N`　→　`N` をどれだけ大きくすれば `K` になる？
- `ceil(x)`　→　小数点があっても上の数に切り上げるよ
