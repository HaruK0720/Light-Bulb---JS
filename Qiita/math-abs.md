# 二点間の距離(マンハッタン距離)　Math.abs　



今回は、二点間の距離を計算する問題を解いた！

ちなみに、マンハッタン距離の由来はアメリカ・ニューヨークの「マンハッタン」の街の構造から来ているらしい。
<br>

## 問題概要

与えられた `N` 個の点 `(x, y)` と、基準点 `(2, 3)` のマンハッタン距離をそれぞれ出力せよ。

マンハッタン距離：
`|x₁ – x₂| + |y₁ – y₂|`

<br>
入力例：

    3
    2 3
    1 2
    5 6

出力例：

    0
    2
    6

### 余談

マンハッタンの道路は、縦と横にまっすぐ通っていて、斜めに進めないので、目的地まで行くには曲がりながら進む必要がある。

そのような状況で使われる距離が「マンハッタン距離」。
✅ よく使われる場面

- 迷路やグリッドマップでの距離計算
- 競技プログラミング
- ルート最適化やゲームAI
- データサイエンス（クラスタリングなど）
<br>

https://paiza.jp/works/mondai/array_primer/array_primer__array_distance_step1NGコード例

<br><br>

## ❌NGコード例
```js
const rl = require('readline').createInterface({input:process.stdin});
const lines = [];

rl.on('line',(input)=>{
    lines.push(input);
});


rl.on('close',()=>{
    const N = Number(lines[0]);
    const coordinate　= lines.slice(1).map(line => line.split(' ').map(Number));
    
    coordinate.forEach(element => {
        const result = (element[0] - 2) + (element[1] - 3);
        console.log(result);
    })
});
```
<Br>

提出コードのアウトプット
```
0
-2
6
```

### ❌問題 ：マンハッタン距離の定義を無視している

上記のコードは絶対値 `| |` をとっていないため、負の値が出ることもあり、正しい距離ではない。
<br><br>

## 📌OKコード例　Math.abs()を使う：
```js
const rl = require('readline').createInterface({ input: process.stdin });
const lines = [];

rl.on('line', input => lines.push(input));

rl.on('close', () => {
    const N = Number(lines[0]);
    const baseX = 2, baseY = 3;

    for (let i = 1; i <= N; i++) {
        const [x, y] = lines[i].split(' ').map(Number);
        const distance = Math.abs(x - baseX) + Math.abs(y - baseY);
        console.log(distance);
    }
});
```
<br>
✅ 解説ポイント

- `Math.abs()`：絶対値をとる関数。マンハッタン距離に必須。

- `split(' ').map(Number)`：座標を `[x, y]` の数値配列に変換。



- 変数名が抽象的すぎるのを修正。
    - `element[0]`, `element[1]` では何の値かパッと見てわからない。
    - `[x, y]` に分割代入したほうが、読み手が内容を理解しやすい。　
- ループで各点にアクセスし、距離を1行ずつ出力。

<br><br>

## 💡新しく学んだことまとめ

- `Math.abs()`は数の絶対値を返してくれる関数。
- 分割代入 `[x, y] = ...` でコードがスッキリ＆理解しやすくなる。
- マンハッタン距離はゲームや地図アプリでも使われる！


<br><br><br>[僕の失敗談(´;ω;｀)と解決法🐈](https://paizabeginner.wordpress.com/2025/05/23/paiza%e3%81%a7%e5%9f%ba%e6%9c%ac%e3%83%9e%e3%82%b9%e3%82%bf%e3%83%bc%ef%bc%9a%e4%ba%8c%e7%82%b9%e9%96%93%e3%81%ae%e8%b7%9d%e9%9b%a2%e3%83%9e%e3%83%b3%e3%83%8f%e3%83%83%e3%82%bf%e3%83%b3%e8%b7%9d/)
