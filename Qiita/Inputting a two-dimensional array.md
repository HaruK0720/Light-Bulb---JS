# 二次元配列の入力

今日は配列メニューの２次元配列の練習問題を解いたのでメモ！

<br>

## 🔍 問題概要

問題：
1行目に列数Mが与えられ、次の5行M列の整数が入力される。

やること：
各行をスペース区切りでそのまま出力。

<br>

入力例:
```
4
1 2 3 4
0 0 0 0
8 1 3 8
1 10 100 99
15 68 48 15
```

出力例:
```
1 2 3 4
0 0 0 0
8 1 3 8
1 10 100 99
15 68 48 15
```
<br>

https://paiza.jp/works/mondai/array_primer/array_primer__2dmatrix_input_step2


## <br><br>💣 NGコード例

```js
const rl = require('readline').createInterface({input:process.stdin});
const lines = [];

rl.on('line',(input)=>{
    lines.push(input);
});


rl.on('close',()=>{
    const matrix = lines.slice(1).map(line => line.split(' '));
    matrix.forEach(a => console.log(a));
});
```
<br>

見た目はOKそう。でも出力はこうなる：
```
[ '1', '2', '3', '4' ]
[ '0', '0', '0', '0' ]
[ '8', '1', '3', '8' ]
[ '1', '10', '100', '99' ]
[ '15', '68', '48', '15' ]
```
このコードは、配列 をそのまま `console.log()` に渡している。
すると、配列を [要素, 要素, …] のように表示されてしまう。

<br><br>

## ✅ OKコード
```js
const rl = require('readline').createInterface({input:process.stdin});
const lines = [];

rl.on('line',(input)=>{
    lines.push(input);
});

rl.on('close',()=>{
    const matrix = lines.slice(1).map(line => line.split(' '));
    
    const result = [];
    
    for(let i = 0; i < matrix.length; i++){
        const row = [];
        for(let j = 0; j < matrix[i].length; j++){
            row.push(matrix[i][j]);
        }
        result.push(row.join(' '));
    }
    
    result.forEach(row => console.log(row));
    
});
```
- 2行目以降をスペースで分割して、2次元配列として取得。
- 各行を1文字ずつループして新しい配列 `row` に再構築。
- 最後に `row.join(' ')`  でスペース区切りの文字列に変換して `result` に追加。
- 配列としてではなく、スペースで連結した文字列を出力するので、期待通りの出力になる。

## <Br>✅改善案
```js
const rl = require('readline').createInterface({ input: process.stdin });
const lines = [];

rl.on('line', input => lines.push(input));

rl.on('close', () => {

    // 2行目以降を2次元配列として格納
    const matrix = lines.slice(1).map(line => line.split(' '));


    // ✅各行をスペース区切りで出力
    matrix.forEach(row => console.log(row.join(' ')));
});
```

<br><br>

## 📘メモ＆まとめ
- `console.log([1, 2, 3])` → `[1,2,3]` になる（配列のまま表示）

- `console.log([1,2,3].join(' '))` → `'1 2 3'` になる（文字列として表示）

- 実行結果が「一見正しそう」でも、形式が違うと評価NGになることもある！

<br><br><br>[僕の失敗談(´;ω;｀)と解決法🐈](https://paizabeginner.wordpress.com/2025/05/18/paiza%e3%81%a7%e5%9f%ba%e6%9c%ac%e3%83%9e%e3%82%b9%e3%82%bf%e3%83%bc%ef%bc%9a%e4%ba%8c%e6%ac%a1%e5%85%83%e9%85%8d%e5%88%97%e3%81%ae%e5%85%a5%e5%8a%9b/)
