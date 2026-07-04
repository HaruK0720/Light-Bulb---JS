# 条件分岐 × 論理式




今回のPaiza問題は、「AND」「OR」を使ってうまくYESを言わせる問題に挑戦してみた！

<Br>


## 🔍問題概要

3つの整数 `X`, `Y`, `Z` が与えられる。

- Zが10以上 → 無条件で YES
- Zが10未満 → X と Y が両方10以上なら YES、どちらか足りなければ NO

<br>

入力例：
    
    15 12 0

出力例：
    
    YES

<br>

https://paiza.jp/works/mondai/conditions_branch/conditions_branch__bool_boss

<br><br>

## コード例：
```js
const rl = require('readline').createInterface({ input: process.stdin });

rl.once('line', (input) => {
    const [x, y, z] = input.split(' ').map(Number);

    let result;
    if (z >= 10) {
        result = "YES";
    } else if (x >= 10 && y >= 10) {
        result = "YES";
    } else {
        result = "NO";
    }

    console.log(result);
    rl.close();
});
```
これでも正解だけど、本問題はOR記号を用いることで 1 回だけの条件分岐で正解することもできる！

<Br><Br>

## ✅ AND + OR

```js
const rl = require('readline').createInterface({ input: process.stdin });

rl.once('line', (input) => {
    const [x, y, z] = input.split(' ').map(Number);

    if ((x >= 10 && y >= 10) || z >= 10) {
        console.log("YES");
    } else {
        console.log("NO");
    }

    rl.close();
});
```
論理演算子 `||`（または）は左側が `false` でも右側が `true` なら全体が `true` になる。

つまり：

`Z >= 10` のとき → `true || …` なので必ず “`YES`”。

`Z < 10` のとき → `x >= 10 && y >= 10` を評価。



### ✅ メリット
- コードが簡潔になる。
- 可読性も高い。

<br><br>

## 📘メモ
- `||`（OR）は 片方が `true` なら全体も `true`
- `&&`（AND）は 両方が `true` でなきゃ `false`
- 条件式は「左 → 右」に評価され、`true` になった時点で終了（短絡評価）
- `if ((A && B) || C)` は、「 `C` が `true` なら `A` や `B` は無視してOK」に使える！

<br>

## まとめ

今後も複数条件を扱うときには、論理演算子の性質（優先順位・短絡評価）を意識すると、スマートなコードが書けそう！


<br><br><br>[僕の失敗談(´;ω;｀)と解決法🐈](https://paizabeginner.wordpress.com/%e8%a8%98%e4%ba%8b%e4%b8%80%e8%a6%a7/)
