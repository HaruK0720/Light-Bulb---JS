# 1を数えよ（2進数）



今回はpaizaの「2進数に変換したときの1の個数を数える」問題に挑戦！

2進数に変換する解き方は最近学習したところ！

<br>

問題概要

与えられた10進数の整数Nを2進数に変換したときの1の個数を出力せよ。

<br>

入力例：

    13

出力例：

    3

<br>

https://paiza.jp/works/mondai/c_rank_skillcheck_archive/count_one_00

<br><br><br>

# ✅ OKコード例：正攻法？
```js
const rl = require('readline').createInterface({input:process.stdin});


rl.once('line', (input) => {
    const N = Number(input);
    
    let binary = [];
    
    
    for(let temp = N; temp > 0; binary.push(temp % 2), temp = Math.floor(temp / 2))
    
    binary = binary.reverse();
    
    
    let count = 0;
    binary.forEach(num => { if (num === 1) count++ });
    
    console.log(count);
    rl.close();
});
```
  
✅ 2で割り続ける
✅ 余りを記録する（0 or 1）
✅ 逆順に並べる

これで、10進数 → 2進数変換ができる！

そこからループと条件分岐で1をカウントして、出力！

<br><br><br>

# 💡 OKコード例 2：
```js
const rl = require('readline').createInterface({input:process.stdin});


rl.once('line', (input) => {
    const N = Number(input);
    
    const count = (N.toString(2).match(/1/g) || []).length;
        
    console.log(count);
});
```

<br><br>


## 💡解説
### ① N.toString(2)

整数 N を 2進数の文字列 に変換する。
```js
N = 13;
N.toString(2); // → "1101"
```
<br>

### ② .match(/1/g)

これは 正規表現で “1” をすべて探すメソッド。

<br>

```js
"1101".match(/1/g); // → ["1", "1", "1"]
```

- `/1/g` は “1” を グローバル（全文）検索
- 結果は 一致した文字を配列にして返す

<br>

### ③ || []

重要なポイント！

`match()`は 一致が見つからないと `null` を返すため、そのまま `.length` を取るとエラーになるから！

<br>

例：
```js
"0000".match(/1/g); // → null
null.length // ❌ TypeError
```
これを防ぐために `|| []` で、`null`のときは空配列にするという保険を書いている。

<br>

### ④ .length

最後に配列の要素数、つまり “1” の個数を数える。
```js
["1", "1", "1"].length → 3
```

<br><br><br>

# 🗒️メモ＆まとめ

- `N.toString(2)`で2進数変換
- `.match(/1/g)` で1を配列に取得
- `null`対策を忘れずに


<br><br><br>[僕の失敗談(´;ω;｀)と解決法🐈](https://paizabeginner.wordpress.com/about/)
