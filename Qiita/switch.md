# 野球の審判　switch




今回は、野球の審判に挑戦！

今 話題の「switch」を使ってみた！

<br>

# 問題概要

- “strike”が3回 → "out!"

- “ball”が4回 → "fourball!"

- それまでは、1～2回目は "strike!" / 1～3回目は "ball!"

<br>


入力例:

    5
    ball
    strike
    ball
    strike
    strike

出力例:

    ball!
    strike!
    ball!
    strike!
    out!

<br>

https://paiza.jp/works/mondai/c_rank_skillcheck_archive/umpire


<br>
<br>
<br>

# ✅ OKコード：
```js
const rl = require('readline').createInterface({ input: process.stdin });

const lines = [];

rl.on('line', (input) => {
  lines.push(input);
});

rl.on('close', () => {
  const judgments = lines.slice(1);

  let strike = 0;
  let ball = 0;

  for (const judge of judgments) {

    if (judge === "strike") {
      strike++;
      if (strike >= 3) {
        console.log("out!");
        break;
      }
      console.log("strike!");
    }

    else if (judge === "ball") {
      ball++;
      if (ball >= 4) {
        console.log("fourball!");
        break;
      }
      console.log("ball!");
    }
  }
});
```
- `for-of` でインデックス管理不要・意図が明確
- `break` で即終了


<br>

## ❌NG例：
```js
if (strike === 3) {
  console.log("out!");
}
console.log("strike!"); // ←3回目でも"strike!"が出ちゃう
```
これ、“out!”の後にも”strike!”って叫ぶ変な審判爆誕。
試合止まらず永遠に判定しちゃう → `break`の必要性がわかる。


<br>
<br>
<br>
<br>
<br>

# 💡switch

これだといつものやり方だし、簡単すぎてつまらないので、新しいメソッドを使ってみる！

<br>

## 💡コード例：
```js
for (const judge of judgments) {

        switch (judge) {
            case 'strike':
                strike++;
                console.log(strike >= 3 ? "out!" : "strike!");
                if (strike >= 3) break; // 終了条件
                break;

            case 'ball':
                ball++;
                console.log(ball >= 4 ? "fourball!" : "ball!");
                if (ball >= 4) break; // 終了条件
                break;
        }

        // この打者の番が終了ならループを抜ける
        if (strike >= 3 || ball >= 4) break;
    }
```

<br>

##  🔍 switch のメリットと注意点

### ✅ 見た目がスッキリ
条件が "strike" や "ball" のように明確な文字列分岐なら switch が読みやすい

### ✅ 拡張しやすい	
"foul" や "hit" のような判定が増えても case を追加するだけ

### ⚠ 条件が複雑なときは不向き	
switch は「一致」のみが対象なので、`x > 3` などの不等式は書けない


<br>

## 💡 補足：break の意味

- `switch` 文では、該当する `case` に入った後に `break` を書かないと、次の `case` に処理が流れてしまう（これを「フォールスルー」と言う）
- `break` は「ここで `switch` を抜けるよ！」という意味。

※フォールスルーは「同じ処理を複数のケースで共有したいとき」に使える。


<br>
<br>

## 🗒️まとめ
### ✅ switch を使うと便利な場面

- 比較対象が「等しいかどうか」だけのとき（例えば文字列、数値など）
- 複数の値に応じて明確に分岐したいとき
- `if` 文が何個も続いて読みにくいとき

### ❌ switch に向いていない場面

- 不等号（例: `x > 10`）などの「範囲比較」が必要なとき
- 複数条件を `&&` や `||` で組み合わせたいとき

<br><br><br>[僕の失敗談(´;ω;｀)と解決法🐈](https://paizabeginner.wordpress.com/about/)
