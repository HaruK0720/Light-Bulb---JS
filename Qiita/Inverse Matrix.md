# 転置行列




転置行列って聞くと一瞬ひるむけど、実はただの「行と列の反転」！

<br>

## 問題概要

N 行 K 列 の2次元配列を、K 行 N 列 の 転置行列 に変換して出力せよ。

<br>

入力例：

    2 3
    1 2 3
    4 5 6

出力例：

    1 4
    2 5
    3 6

<br>

https://paiza.jp/works/mondai/double_roop_problems/double_roop_problems__transposition

<br><br><br>

## 🟥 NG例
```js
const rl = require('readline').createInterface({input:process.stdin});
const lines = [];

rl.on('line', (input) => {
    lines.push(input);
});


rl.on('close', () => {
    const [N, K] = lines[0].split(' ').map(Number);

    const arrA = lines.slice(1).map(line => line.split(' '));
    
    for(let i = 0; i < N; i++){
        const row = [];
        
        for(let j = 0; j < K; j++){
            row.push(arrA[i][j]);
        }
        
        console.log(row.join(' '));
    }
    
});
```
👉 これだとただの出力。行と列の立場逆転をしないと転置にはならない！

<br><br>

## 🟩 OK例①：for文で正攻法
```js
for(let i = 0; i < K; i++){
    const row = [];
    for(let j = 0; j < N; j++){
        row.push(arrA[j][i]);
    }
    console.log(row.join(' '));
}
```
✅ 解説：外ループが元の列番号＝転置後の行、内ループが元の行＝転置後の列。

<br><br>

## 🟨 OK例②：Array.from
```js
const transposed = Array.from({ length: K }, (_, i) =>
  Array.from({ length: N }, (_, j) => arrA[j][i])
);

transposed.forEach(row => console.log(row.join(' ')));
```

✅ 解説
`Array.from({ length: K }, (_, i) => …)`

- 長さ K の配列（転置後の行数）を作る。
- i は転置行のインデックス。

`Array.from({ length: N }, (_, j) => arrA[j][i])`
- その行を構成するために、元の配列の各行から i 番目の値を集める。

<br><br>

## 🟦 OK例③：map()
```js
const transposed = arrA[0].map((_, i) => arrA.map(row => row[i]));

transposed.forEach(row => console.log(row.join(' ')));
```
✅ 解説
`arrA[0].map((_, i) => …)`    
- 最初の行から 列数分だけループさせる。
- `i` が列インデックス（転置後の行インデックス）。

`arrA.map(row => row[i])`
- 各行から `i` 番目の要素を抜き出して、列 → 行にする。

<br><br><br>

## 📝メモ＆学んだことまとめ

- `Array.from({ length }, (_, i) => ...)` の使い方（配列初期化に便利）
- 2次元配列の扱い方、行→列の切り替えのロジック
- 高階関数（ `.map()` ）が2重でも思ったより読める


<br><br><br>[僕の失敗談(´;ω;｀)と解決法🐈](https://paizabeginner.wordpress.com/2025/06/16/paiza%e3%81%a7%e5%9f%ba%e6%9c%ac%e3%83%9e%e3%82%b9%e3%82%bf%e3%83%bc%ef%bc%9a%e8%a1%8c%e5%88%97%e3%81%ae%e8%bb%a2%e7%bd%ae/)
