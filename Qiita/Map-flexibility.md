# パスワード作成　Mapの柔軟性

Paizaの指定されたルールに則ってパスワードを作る問題を解いた！
「value＝数値」という固定観念を打破した気づきは、Mapの強みを理解する大事な一歩だった！

<br>

## 🔍 問題概要

問題：「N文字のパスワードを作れ。ただしQ個の位置と文字が決まってて、残りはCで埋めること。」

例：N = 5, Q = 1, 指定「2文字目 = "T"」、C = "K" → KTKKK

入力例
```
5
1
2 T
K
```
出力例
```
KTKKK
```
<br>

https://paiza.jp/works/mondai/string_primer/advance_step6



## <br><br> NG例：初めのコード
```js
const rl = require('readline').createInterface({input:process.stdin});
const lines = [];

rl.on('line',(input)=>{
    lines.push(input);
});

rl.on('close',() => {
    const N = Number(lines[0]);
    const Q = Number(lines[1]);
    const C = lines[Q+2];
    
    const linesQ = lines.slice(2,Q+2).map(line => line.split(' '));
    
    const password = [];
    for(let i = 1; i <= N; i++){
        if(linesQ.includes(String(i))){
            password.push(linesQ[i][1]);
        }
        
        else{
            password.push(C);
        }
    }
    
    console.log(password.join(''));
});
```
### ❌ 問題点
`linesQ.includes(String(i))` は常に `false` であること。

- `linesQ` は `[ [ '1', 'A' ], [ '3', 'Z' ] ]` のような「配列の配列」(２次元配列)。

- `includes(String(i))` で "1" のような文字列を探しても、`linesQ` の中にそのような単一の文字列要素はないため `false` になる。

<br><br><br>

## ✅ OKコード（Mapで解決）
```js
const rl = require('readline').createInterface({ input: process.stdin });
const lines = [];

rl.on('line', (input) => {
    lines.push(input);
});



rl.on('close', () => {
    const N = Number(lines[0]);
    const Q = Number(lines[1]);
    const C = lines[Q + 2];

    const queries = lines.slice(2, Q + 2).map(line => {
        const [index, char] = line.split(' ');
        return [Number(index), char];
    });

    // インデックスを key、文字を value にする Map を作成
    const map = new Map();
    queries.forEach(([index, char]) => {
        map.set(index, char);
    });

    // パスワードを構築
    const password = [];
    for (let i = 1; i <= N; i++) {
        if (map.has(i)) {
            password.push(map.get(i));
        } else {
            password.push(C);
        }
    }

    console.log(password.join(''));
});
```
解説:

- `Map` で `key` : 位置 → `value` : 文字 として保存

- `map.has(i)` で存在チェック、なければ `C` を入れる

- `join('')` でパスワード完成！

<br>

## ✏️ 気づきメモ

- `配列.includes()` で多次元配列の中身は探せない（配列ごと一致する要素しか探せない）

- キー検索には `Map` やオブジェクトが向いてる

<br>

💡 `Map`では、キーだけでなく値（`value`）にも数値以外の「文字列」「オブジェクト」「関数」などが入れられる！ 
 → 僕は「`value` ＝ 数値」っていう固定観念にとらわれてたけど、完全に誤解だった(´;ω;｀)

<br><br>

## 🏁 まとめ
初心者の僕でも、`Map`を使えばスッキリ解けました。
失敗は成功のもと、というより失敗こそが教材。`Map`の柔軟性を知れたのは大きな一歩！

<br><br>
[
🐈僕の失敗談と解決話！🐻](https://paizabeginner.wordpress.com/2025/05/05/paiza%e3%81%a7%e5%9f%ba%e6%9c%ac%e3%83%9e%e3%82%b9%e3%82%bf%e3%83%bc%ef%bc%9a%e3%83%91%e3%82%b9%e3%83%af%e3%83%bc%e3%83%89%e4%bd%9c%e6%88%90%e3%80%80map%e3%81%ae%e6%9f%94%e8%bb%9f%e6%80%a7/)
