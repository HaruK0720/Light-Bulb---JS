# 数値判定　isNaNの罠に注意せよ！


Paizaの文字列処理の「数値判定」問題を解いたので落とし穴と解決法を交えて解説！

## <br>問題概要

文字列 `S` が与えられるので、 `S` を整数に変換できる場合には “`YES`” , そうでない場合は “`NO`” を出力。

なお、文字列 S を数値に変換できるとは、S の全ての文字が
{ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 } のいずれかであることをいう。

 S の各文字は数字（{ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 } のいずれか) またはアルファベットの大文字。
 
```
入力例：
813

出力例：
YES
```
<br>

https://paiza.jp/works/mondai/string_primer/advance_step4


<br>

## コード例①
```js
const rl = require('readline').createInterface({input:process.stdin});

rl.once('line',(input)=>{
    if(!isNaN(input)){
        console.log("YES");
    } else {
        console.log("NO");
    }
});
```

### ❗ 罠ポイント

- `isNaN("")` → `false` →（ `Number("")` → `0` ）→ `YES`
- `isNaN(" ")` → `false` →（ `Number("")` → `0` ）→ `YES`
- 指数表記（例: `"123E4"`）も `false` になり、誤って `YES`



空白や空文字だけでも `YES` になる可能性があるという地味に怖い仕様。
<br>
※今回の問題は、空文字や空白はないので大丈夫。

<br>

## ✅ 改善コード（3段チェックで堅牢に）
```js
const trimmed = input.trim();
const isNumber =
  trimmed !== "" &&
  !isNaN(trimmed) &&
  !isNaN(Number(trimmed)) &&
  !/[eE]/.test(trimmed);

console.log(isNumber ? "YES" : "NO");
```

### ✔ 解説（3つのチェック）

- `trimmed !== ""` → 空文字の排除
- `!isNaN(trimmed)` → 数値変換チェック（型変換あり）
- `!isNaN(Number(trimmed))` → 明示的に数値変換 → `NaN` 判定
- `!/[eE]/.test(trimmed)` → 指数表記の "e" または "E" を排除


<br>

さらに、`&&`の短絡評価を使って、効率的にチェック!

`&&` は論理積（AND）演算子で、左から右へ評価を行う。
各条件が `true` の場合に次の条件を評価し、
最終的にすべての条件が `true` であれば全体が `true` になる。
途中で `false` が出た時点で評価を終了（短絡評価）。

<br>

## 💡 新しく学んだこと

- `trim()`：前後の空白を削除
- `!== ""`：空文字は除外
- `!isNaN(…)`：数値に変換できるか確認
- 入力系の問題では「予期しない入力」に注意

<br>

## ✅ まとめ

空文字や空白のみの入力、数値と文字が混在する入力などを適切に除外し、正確な数値判定が可能になる！

このような細かな判定を行うことで、予期しないエラーを防ぐことができる👍


<br><br><br>[🐻 僕の失敗談と解決話！](https://paizabeginner.wordpress.com/2025/05/04/paiza%e3%81%a7%e5%9f%ba%e6%9c%ac%e3%83%9e%e3%82%b9%e3%82%bf%e3%83%bc%ef%bc%9a%e6%95%b0%e5%80%a4%e5%88%a4%e5%ae%9a%e3%80%80isnan%e3%81%ae%e7%bd%a0%e3%81%ab%e6%b3%a8%e6%84%8f%e3%81%9b%e3%82%88%ef%bc%81/)
