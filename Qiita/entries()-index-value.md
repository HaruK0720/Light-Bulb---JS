# 1 はどこにある？


今回はPaizaの「配列の中の1の位置を全部出す問題」に挑戦！

前回学んだ `entries()` を使ってみたけど、順番とインデックスのズレでちょっとつまづいた…(´;ω;｀)

<br>

## 問題概要

- N個の整数が与えられる
- a_1 を 1番目とし、配列に必ず1が含まれる
- 1 がある位置を先頭から順に改行区切りで出力

<br>


入力例：

    5
    5 3 1 3 5

出力例：

    3

<br>

https://paiza.jp/works/mondai/loop_problems2/loop_problems2__seq_one

<br><br><br>

## ❌NG例
```js
const rl = require('readline').createInterface({input:process.stdin});

const lines = [];

rl.on('line', (input) => {
    lines.push(input);
});


rl.on('close', () => {
    const N = Number(lines[0]);
    const nums =  lines[1].split(' ').map(Number);
    
    
    for(const [value, index] of nums.entries()){
        if(value === 1){
            console.log(index);
        }
    }
});
```
→ インデックスと値の取り方が逆！さらに0始まりのまま出力してるからズレる。

<br><br>

## ✅OK例
```js
for(const [index, value] of nums.entries()){
    if(value === 1){
        console.log(index + 1);
    }
}
```
→ こっちは正しく[インデックス, 値]を取って「+1」して出力。バッチリ！

<br>

## ✅OK例（王道forループ）
```js
for(let i = 0; i < N; i++){
    if(a[i] === 1){
        console.log(i + 1);
    }
}
```
→ シンプルで初心者にも分かりやすい！

<br><br>

## 📝気づきメモ

 - `entries()` は `[index, value]` の順番で受け取る。

- 配列のインデックスは0始まりだから、答えは必ず「+1」すること！

- 基本の for ループも使いこなせるようにする。


<br><br><br>[僕の失敗談(´;ω;｀)と解決法🐈](https://paizabeginner.wordpress.com/2025/06/12/paiza%e3%81%a7%e5%9f%ba%e6%9c%ac%e3%83%9e%e3%82%b9%e3%82%bf%e3%83%bc%ef%bc%9a1-%e3%81%af%e3%81%a9%e3%81%93%e3%81%ab%e3%81%82%e3%82%8b%ef%bc%9f/)
