# 平均以上の数を列挙　reduce()とfilter()



Paizaの「平均以上の値を出力する問題」に挑戦したら、配列メソッドの使い分けがめっちゃ学びになったので、まとめる！
<br>

## 📝 問題内容

1行目に整数 `N`
2行目に `N` 個の整数が与えられる。

この `N` 個の整数のうち、平均以上の値をすべて出力するという問題
<br>

入力例：

    5
    1 2 3 4 5

出力例る：

    3
    4
    5
<br>

https://paiza.jp/works/mondai/array_primer/array_primer__array_ave_step3

<br><br>

## ✅ 解法その1：forEachで1つずつチェック
```js
const rl = require('readline').createInterface({ input: process.stdin });
const lines = [];

rl.on('line', (input) => {
    lines.push(input);
});


rl.on('close', () => {
    const N = Number(lines[0]);
    const nums = lines[1].split(' ').map(Number);

    let total = 0;
    nums.forEach(num => total += num);

    const average = total / N;

    nums.forEach(num => {
        if (num >= average) {
            console.log(num);
        }
    });

});
```
解説：

- `forEach()` で2回ループを回している
    - 1回目で合計を出し、
    - 2回目で平均以上の値をチェックして出力。
     
- 直感的にわかりやすくて、初心者にもおすすめの書き方！

## <br>✅ 解法その2：filter()＋forEach()でスリムに
```js
const rl = require('readline').createInterface({ input: process.stdin });
const lines = [];

rl.on('line', (input) => {
    lines.push(input);
});


rl.on('close', () => {
    const nums = lines[1].split(' ').map(Number);
    const average = nums.reduce((sum, num) => sum + num, 0) / nums.length;

    nums
        .filter(num => num >= average)
        .forEach(num => console.log(num));

});
```
解説：

- `reduce()` で一発で合計を出して平均を計算。
- `filter()` で平均以上の要素だけを抽出。
- そのまま `forEach()` で順番通りに出力。

<Br><br>

## 🎓 新しく学んだことまとめ

### reduce()：
- 配列の要素を累積的に処理して、1つの値にまとめる。
- 合計や積など、累積系処理に大活躍！

書き方↓
```js
array.reduce((acc, cur) => acc + cur, 初期値);
```


### filter()：
- 条件に合う要素だけを残して、新しい配列を作る。



<br><br><br>[僕の失敗談(´;ω;｀)と解決法🐈](https://paizabeginner.wordpress.com/2025/05/22/paiza%e3%81%a7%e5%9f%ba%e6%9c%ac%e3%83%9e%e3%82%b9%e3%82%bf%e3%83%bc%ef%bc%9a%e5%b9%b3%e5%9d%87%e4%bb%a5%e4%b8%8a%e3%81%ae%e6%95%b0%e3%82%92%e5%88%97%e6%8c%99%e3%80%80reduce%e3%81%a8filter/)
