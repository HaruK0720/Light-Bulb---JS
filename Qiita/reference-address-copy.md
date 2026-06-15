# なぜsort()で全部変わる？参照・アドレス・コピーをまとめて理解！



今回解いたのは配列の最大値と最小値を出すだけの問題。

JavaScriptで配列を扱っていて、`sort()`を使ったら他の変数の中身まで変わってしまった…。その理由は、「参照」と「メモリのアドレス」にあった！

<br>

## 問題概要

`N` 個の整数が与えられるので、最大の数と最小の数を半角スペース区切りで出力せよ。

`N` 個の整数を大きい順や小さい順に並び替える操作を考えて解いてみよう。

<br>

入力例:

    5
    1 3 5 2 4

出力例：

    5 1
<br>

https://paiza.jp/works/mondai/array_primer/array_primer__array_minmax

<br><br>

## 📌Math.maxメソッドを使う　
```js
const rl = require('readline').createInterface({input:process.stdin});
const lines = [];

rl.on('line',(input)=>{
    lines.push(input);
});

rl.on('close',()=>{
    const N = Number(lines[0]);
    const nums = lines[1].split(' ').map(Number);
    
    const Max = Math.max(...nums);
    const Min = Math.min(...nums);
    
    console.log(Max, Min)
    
});
```
`...nums` で配列の中身を個別の値に展開して渡す。

<br>

## 📌sort()を使ったバージョン

`N` 個の整数を大きい順や小さい順に並び替える操作を考えて解いてようとのことだったので、考えてみた！
<br>

### NG例：
```js
const N = Number(lines[0]);
const nums = lines[1].split(' ').map(Number);
    
const asc = nums.sort((a,b) => a - b);
const desc = nums.sort((a,b) => b - a);

console.log(desc[0], asc[0]);❌ 両方降順になる
```
なぜか両方とも `[5, 4, 3, 2, 1]` に！？！？！？

<br><br>

### メモリと参照：sort()が他の変数にも影響する理由とは？
#### 🔍 メモリとアドレスって何？

JavaScriptでは、配列やオブジェクトなどの複雑なデータは「値」ではなく「アドレス（場所）」を変数が保持する。

たとえば、次のように配列を作成したとする。
```js
let nums = [3, 1, 2];
```

このとき、配列そのものはメモリ上のどこか（例: 0x1234）に保存される。

そして、変数 `nums` はその「場所（アドレス）」を覚えているだけ。
<Br><br>
### 🧠 図解①：配列の作成
```
メモリ:
アドレス 0x1234: [3, 1, 2]

変数:
nums → 0x1234（配列 [3, 1, 2] を指す）
```
<br><br>

### 🧪 asc にコピーしてみる
```js
let asc = nums;
```
これで `asc` は `nums` と同じアドレス（0x1234）を参照。
<br><br>

### 🧠 図解②：参照のコピー
```
メモリ:
アドレス 0x1234: [3, 1, 2]

変数:
nums → 0x1234  
asc  → 0x1234
```
ここが重要！ → `asc` と `nums` は同じデータを見ている！
<br><br>

### 🔁 sort()をするとどうなる？
```js
nums.sort((a, b) => a - b); // 昇順 → [1, 2, 3]
```
この時、配列の中身自体（アドレス 0x1234 の内容）が書き換えられる。
<br><br>

### 🧠 図解③：sort()の影響
```
メモリ:
アドレス 0x1234: [1, 2, 3]

変数:
nums → 0x1234  
asc  → 0x1234  ←中身が変わってる！
```
つまり `asc` の中身も一緒に変わってしまう。
<br>

### 😱 別の変数でもっと混乱！
```js
let desc = nums.sort((a, b) => b - a); // 降順 → [3, 2, 1]
```
この `sort()` も同じアドレスを操作しているため…

<br><br>

### 🧠 図解④：すべて同じ配列に
```
メモリ:
アドレス 0x1234: [3, 2, 1]

変数:
nums → 0x1234  
asc  → 0x1234  
desc → 0x1234
```

結果：`nums`, `asc`, `desc` は全部同じデータになってしまう！
<Br><br>

### ✅ 対策：スプレッド構文でコピーを作ろう！
```js
let asc = [...nums].sort((a, b) => a - b);   // 昇順コピー
let desc = [...nums].sort((a, b) => b - a);  // 降順コピー
```
これで `nums` の元データは変わらず、`asc` や `desc` は別のアドレスを持つ独立した配列になる！
<br><br>

### 💡 ポイントまとめ
- `sort()` で他の変数も変わる　→　同じ配列（アドレス）を共有しているから
- `let b = a` でコピーにならない　→　値ではなく参照（アドレス）がコピーされる
- スプレッド構文  `[...a]` や `.toSorted()` で配列のコピーを作る

<br><br>

## ✅OKコード完成例：

```js
const rl = require('readline').createInterface({ input: process.stdin });
const lines = [];

rl.on('line', (input) => {
    lines.push(input);
});

rl.on('close', () => {
    const N = Number(lines[0]);
    const nums = lines[1].split(' ').map(Number);


    // 昇順ソート（最小値）
    const asc = [...nums].sort((a, b) => a - b);   

    // 降順ソート（最大値）
    const desc = [...nums].sort((a, b) => b - a);  


    console.log(desc[0], asc[0]);
});
```

## まとめ：
- `Math.max(nums)` は `NaN` を返すので、`Math.max(…nums)` で展開する
- `sort()` は破壊的 → コピーしてから使おう！
- スプレッド構文や `.toSorted()` を使う。
- 配列は参照型で、変数は配列の『アドレス』を指す

配列を扱うときは、「コピーするかどうか」を意識するのが大事ってことを学んだ！

<br><Br><br>[僕の失敗談(´;ω;｀)と解決法🐈](https://paizabeginner.wordpress.com/2025/05/21/paiza%e3%81%a7%e5%9f%ba%e6%9c%ac%e3%83%9e%e3%82%b9%e3%82%bf%e3%83%bc%ef%bc%9a%e3%81%aa%e3%81%9csort%e3%81%a7%e5%85%a8%e9%83%a8%e5%a4%89%e3%82%8f%e3%82%8b%ef%bc%9f%e5%8f%82%e7%85%a7%e3%83%bb%e3%82%a2/)
