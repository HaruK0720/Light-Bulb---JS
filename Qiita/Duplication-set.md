# 重複を削除する手法 【比較、Set()】

今日はPaizaの「重複削除して出力」問題に挑戦してみた。


## <br>🧩 問題概要

- `N` 個の要素からなる昇順の数列 `A` が与えられます。
- 重複を削除して昇順に出力してください。

<br>入力例:
```
6
1 2 3 3 4 5
```
出力例:
```
1 2 3 4 5
```
<br>

https://paiza.jp/works/mondai/data_structure/data_structure__set_step2

## <br>🔸 方法①：前の数値と比べて違うときだけ出力
```js
const rl = require('readline').createInterface({ input: process.stdin });
const lines = [];

rl.on('line', input => lines.push(input));
rl.on('close', () => {
    const N = Number(lines[0]);
    const A = lines[1].split(' ').map(Number);


    // 結果を格納するための配列（重複なし）
    const result = [];

    // 直前に見た値を保持する変数（最初は null にしておく）
    let prev = null;

    // 配列 A の各要素を順にチェック
    A.forEach(num => {
    
    // 直前の値と違う場合のみ、結果に追加
    if (num !== prev) {
        result.push(num); // 重複していない値を追加
        prev = num;       // 現在の値を次のループの比較用に保存
    
    }

    console.log(result.join(' '));
    
});
```
✅ ソートされてる前提を利用して、隣り合う要素だけ見ればOK。

✅ メモリ効率も良く、`Map`や`Set`を使わずにすむ。

## <br>🔸 方法②：Set を使う
```js
const rl = require('readline').createInterface({ input: process.stdin });
const lines = [];

rl.on('line', input => lines.push(input));

rl.on('close', () => {
    const A = lines[1].split(' ').map(Number);
    const unique = [...new Set(A)]; // Setで重複削除

    console.log(unique.join(' '));
});
```
✅ `Set` は自動的に重複を排除してくれる。

⚠ ソートは保証されないけど、元の配列が昇順だからそのまま出力してOK！


### <br>✨ 超ざっくり一行で書くと？
```js
console.log([...new Set(lines[1].split(' '))].join(' '));
```

## <br>🎓 まとめ
「重複を削除」って一見シンプルだけど、方法によって全然コードの印象が変わる！

<br><br>[僕の失敗談と解決話！](https://paizabeginner.wordpress.com/2025/04/21/paiza%e3%81%a7%e5%9f%ba%e6%9c%ac%e3%83%9e%e3%82%b9%e3%82%bf%e3%83%bc-%e9%87%8d%e8%a4%87%e3%82%92%e5%89%8a%e9%99%a4%e3%81%99%e3%82%8b3%e6%89%8b%e6%b3%95%e3%80%90set%e3%80%81%e6%af%94%e8%bc%83/)

## <br><br>おまけ解説
`[...new Set(A)]` は、重複のない配列を簡単に作れる魔法のような一文✨

一つずつ分解！

✅ `Set(A)` の意味
```js
new Set(A)
```
<br>

`Set` は 重複のない値だけを保持するコレクション型。

たとえば：
```js
const A = [1, 2, 2, 3];
const s = new Set(A); // Set(3) {1, 2, 3}
```
<br>

✅ ポイント
- `Set` に同じ値を2回入れても1個にまとめられる！
- 順序は 最初に出てきた順 を保ってくれる。

<br>✅ `[...Set]` の意味
```js
[...new Set(A)]
```
これは「`Set` を配列に戻す」って意味。
`...`（スプレッド構文）は、中身を取り出して展開してくれる。

たとえば：
```js
const s = new Set([1, 2, 3]);
const arr = [...s]; // [1, 2, 3]
```
<br>

✅ 全体まとめると
```js
[...new Set(A)]
```
これは、
- 配列 `A` を `Set` にして重複を除き
- 再び配列に戻す

つまり「`A` から重複を除いた配列を作る」ってこと！



