# 論理演算を用いた計算　 ド・モルガンの法則

Paizaで「論理演算」の最終問題に挑戦！　
「ド・モルガンの法則」を知ったらスマートな式になる！

## <br>🎯問題

問題：A, B, C, D（各0か1）が与えられたとき、


![02.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4018208/f49ba821-b96a-4db0-b916-51fc41d0662a.png)



の値を出力せよ！

<br>

https://paiza.jp/works/mondai/logical_operation/logical_operation__basic_boss


## <br>💻コード例
### ①そのまま

```js
const rl = require('readline').createInterface({input:process.stdin})

rl.on('line', (input) => {
    const [A,B,C,D] = input.split(' ').map(Number);
    
    console.log( !((!A & !B) | !C) ^ D);
    
    rl.close();
});
```
<br>

### ②ド・モルガン登場！ 簡潔な式に！
```js
const rl = require('readline').createInterface({input:process.stdin})

rl.on('line', (input) => {
    const [A,B,C,D] = input.split(' ').map(Number);
    
    console.log((A | B) & C ^ D);
    
    rl.close();
});
```

#### ✨ 解説

Step変形:
```
!((!A & !B) | !C)
= !(!A & !B) & !!C
= (A | B) & C
```
なので全体は：
```
(A | B) & C ^ D
```

`!!C` は `C` と同じなので省略OK。

## <br>📌 気づきメモ　まとめ

- `!!x = x` は地味だけど覚えとくと便利
- `^`（XOR）は分配法則を持たない。だから `(A | B) & (C ^ D)` みたいな変形は不可
- 論理演算は「数学っぽい」けど、「可読性ファースト」で書くとバグ減る

<br><br>[僕の失敗談(´;ω;｀)と解決法🐈🐻🦁](https://paizabeginner.wordpress.com/2025/05/02/paiza%e3%81%a7%e5%9f%ba%e6%9c%ac%e3%83%9e%e3%82%b9%e3%82%bf%e3%83%bc%ef%bc%9a%e8%ab%96%e7%90%86%e6%bc%94%e7%ae%97%e3%82%92%e7%94%a8%e3%81%84%e3%81%9f%e8%a8%88%e7%ae%97%e3%80%80%e3%83%89%e3%83%bb/)

<br><br><br>

## おまけ：　💡ド・モルガンの法則とは？

2つの基本形があります：
### ✅ 1. 否定がANDにかかっているとき：
```
!(A && B) ≡ (!A || !B)
```
「AとBの両方じゃない」は、「Aじゃない か Bじゃない」
<br>

### ✅ 2. 否定がORにかかっているとき：
```
!(A || B) ≡ (!A && !B)
```
「AまたはBじゃない」は、「AもBもじゃない」

### 例：
```
元の式:

!((!A & !B) | !C)

変形:

= !(!A & !B) & !!C
= (A | B) & C   ←スッキリ！
```

### 💡 なぜ便利？

- 長い論理式を 簡単に＆読みやすく 書き直せる
- 条件分岐や論理演算問題を 論理的に変形できる
- 回路設計（AND/ORゲート）の基本法則でもある

### 🧪 まとめ

ド・モルガンの法則を覚えると、「条件の否定」や「論理演算の整理」がめちゃくちゃスムーズになる！

覚え方はシンプルに：
「`!`（NOT）が中に入ると、演算子（AND ⇔ OR）が逆になる！」
