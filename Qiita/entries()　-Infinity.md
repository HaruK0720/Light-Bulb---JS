# 加算された数列の最大値　.entries()　-Infinity


Paizaの「`a[i] + i` の最大値を求める」問題に挑戦したときの学習を記録！

<br>

## 問題概要

- N 個の整数 a_1, a_2, …, a_N が与えられる。
- a_i に i を足したとき、a_1 , … , a_N の最大値を出力せよ。

<br>

入力例：

    5
    1 2 3 4 5

出力例：

    10

<br>

https://paiza.jp/works/mondai/loop_problems2/loop_problems2__add_maxseq

<br><br><br>

## ✅ OK例：Math.max() + 配列
```js
const rl = require('readline').createInterface({input:process.stdin});
const lines = [];

rl.on('line', (input) => {
    lines.push(input);
});


rl.on('close', () => {
    const N = Number(lines[0]);
    const nums = lines[1].split(' ').map(Number);
    
    let sum = [];
    for(let i = 1; i <= N; i++){
        sum.push(nums[i-1] + i);
    }
    
    console.log(Math.max(...sum));
});
```

`.push()` で計算結果を全部入れてから `Math.max(...sum)` で最大値を取るやり方。
これは「結果を配列に残したい」ってときに便利。

<br>

### 💡 .entries()

インデックスも値も同時にほしいときは `.entries()` を使うと良い！

`for-of` だと通常「値」しか取れないけど、

`.entries()` は [インデックス, 値] のペアを返してくれるから、
<br>

```js
for(const [index, value] of nums.entries()) {
    sum.push(value + index + 1);
}
```
って書ける。 `index` は 0 始まりだから +1 して i に合わせてるよ。

<br><br><br>

## ✅ sum 配列なしでも最大値だけでOK！

実は、最大値だけほしいなら sum 配列すらいらない。直接更新しながら最大値を求める方法がスマート！
```js
let maxVal = -Infinity;
for(let i = 1; i <= N; i++) {
    const current = nums[i - 1] + i;
    if(current > maxVal) {
        maxVal = current;
    }
}
console.log(maxVal);
```

`-Infinity` って「どんな数よりも小さい」特別な値。

これを使うと「最初に比べる相手がいない」ってときに超便利。順に比べながら更新していくやつだね！

<br><br><br>

## 📝 メモ

- 配列インデックスは 0 から始まるけど、問題は 1 から始まる。ズレに注意！
- `.entries()` は配列操作で「インデックスと値」を同時に扱うのに超便利。
- 最大値だけほしいなら「一時配列 sum を作らず、比較しながら更新」でOK！
- 最小値スタートの `-Infinity` は「どんな数よりも小さい」という覚え方でイメージしやすい。



<br><br><br>[僕の失敗談(´;ω;｀)と解決法🐈](https://paizabeginner.wordpress.com/2025/06/11/paiza%e3%81%a7%e5%9f%ba%e6%9c%ac%e3%83%9e%e3%82%b9%e3%82%bf%e3%83%bc%ef%bc%9a%e5%8a%a0%e7%ae%97%e3%81%95%e3%82%8c%e3%81%9f%e6%95%b0%e5%88%97%e3%81%ae%e6%9c%80%e5%a4%a7%e5%80%a4/)
