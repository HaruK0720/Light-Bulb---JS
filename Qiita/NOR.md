# NOR 演算の基本 !(A | B) 　　おまけ:| と || の違い

0と1しか出てこないのに、なぜかめちゃくちゃ奥が深い…。
今回解いたのは、Paizaの「NOR演算」

## <br>🧩 問題概要：
入力は `0` `1` の2つの数値で、出力は NOR（NOT OR）の結果。

<br>

https://paiza.jp/works/mondai/logical_operation/logical_operation__basic_step6


## <br>NGコード：
```js
const result = !(A | B);
console.log(result); // ❌ true or false が出る
```
これは論理値（boolean）を出してるだけ。
数値（0か1）で出さないとジャッジが通らない

## <br>✅ OKコード：
```js
const [A, B] = require("fs").readFileSync("/dev/stdin", "utf8").trim().split(" ").map(Number);
const result = Number(!(A | B));
console.log(result); // ちゃんと 0 or 1！
```
- `A | B` はビットOR

- `!` はNOT

- `Number()` が `true` / `false` を `1` / `0` に変換

<br>

NORも万能ゲートらしい
例：
- NOT A = A NOR A
- A OR B = (A NOR B) NOR (A NOR B)
- A AND B = (A NOR A) NOR (B NOR B)

NORだけで全ての論理演算を再現できる

## <br>📌 まとめ
NORは「ORの否定」と覚えればいい！

<br><br> [僕の失敗談(´;ω;｀)と解決策🐈🚀](https://paizabeginner.wordpress.com/2025/04/28/paiza%e3%81%a7%e5%9f%ba%e6%9c%ac%e3%83%9e%e3%82%b9%e3%82%bf%e3%83%bc%ef%bc%9anor-%e6%bc%94%e7%ae%97%e3%81%ae%e5%9f%ba%e6%9c%ac-a-b-%e3%81%8a%e3%81%be%e3%81%91-%e3%81%a8-%e3%81%ae%e9%81%95/)

## <br>おまけ ： JavaScriptにおける | と || の違い、まとめてみた👇

### ✅ |（ビット単位の OR）

ビット演算子（Bitwise OR） ってやつ。

各ビットごとに比較して、どちらかが1なら1を返す

例：
```js
console.log(5 | 3);  // => 7
// 5 = 0101
// 3 = 0011
// ---------
//     0111 = 7
```


### <br>✅ ||（論理 OR）

論理演算子（Logical OR） ってやつ。

- 左が「truthy」ならそれを返す。
- 左が「falsy」なら右を評価してそれを返す。
-「条件分岐」でよく使う！

例：
```js
console.log(true || false);      // => true
console.log(0 || 100);           // => 100
console.log("hello" || "world"); // => "hello"
```

### <br>👀 補足：今回の論理演算にはどっち？

Paizaの「0か1の論理演算」系は、0か1の数値として処理されるから：

`|` や `&` など ビット演算子を使うのがいいかも。
（でも `||` や `&&` を使っても 0と1なら正しく動いちゃう ）

📌 例：混乱しやすいやつ
```js
console.log(0 | 1);   // => 1  ← 数値（ビット演算）
console.log(0 || 1);  // => 1  ← 真偽値判定（0は falsy）

//でも：

console.log(0 || 2);  // => 2 ← 条件っぽく動く
```

「演算として使う」のか、「条件として使う」のか、そこが判断の分かれ目！
