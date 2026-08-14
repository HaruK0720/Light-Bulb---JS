# 論理演算子の優先順位


今回は条件分岐の問題に挑戦！論理演算子に優先順位があるんだと初めて知った！

<br>

# 問題概要

整数A, B, C, Dが与えられる。

- AとBが等しい　または 　CとDが等しい
- かつ AとCが等しい

この2つの条件がともに真のとき、またそのときに限り真となる条件式を書くがいい！

<br>

入力例：

    1 1 1 2

出力例：

    1

<br>

https://paiza.jp/works/mondai/conditions_expression/conditions_expression__logical_operator_boss

<br><br><br>



# ❌NGコード：
```js
const rl = require('readline').createInterface({input:process.stdin});


rl.once('line', (input) => {
    const [A, B, C, D] = input.split(' ').map(Number);
    
    console.log(A === B || C === D && A === C);
    
    
    rl.close();
});
```

<br><br>

# ✅ OKコード：
```js
console.log((A === B || C === D) && A === C);
```

<br><br>

# 💡論理演算子の優先順位

この問題のポイントは「論理演算子の優先順位」！

<br>

`&&`（AND）は `||`（OR）よりも優先順位が高い。

つまり `A || B && C`  は  `A || (B && C)` として扱われてしまったことによって、
❌不正解となった…(´;ω;｀)

<br><br><br>

## ✅ 解決策：迷ったら括弧 ( ) を使おう！

複雑な条件やミスが起きそうなときは、優先順位を明示するために `()` を使うのがベスト！

<br>

```js
if ((A === B || C === D) && A === C) { ... }
```

OR を先に評価したい → `()` で囲む！

<br><br><br>


## 📝論理演算子の優先順位（高い順）
```
!  >  &&  >  ||
```
- `!`（NOT）が最優先
- 次に `&&`（AND）
- 最後に `||`（OR）

<br><br><br>

# 🗒️まとめメモ

- `&&`（AND）は `||`（OR）よりも優先順位が高い 
 
- `()`で優先順位を指定するとよい
- 比較は `==` でもOKだけど、厳密等価 `===` を使うのがベスト




<br><br><br>[僕の失敗談(´;ω;｀)と解決法🐈](https://paizabeginner.wordpress.com/about/)
