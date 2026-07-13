# FizzBuzz問題 いろんな解き方


今回はPaizaの「条件分岐 – FizzBuzz」問題にチャレンジ！過去に解いたことがあるけど、今度はほかの解き方も考えてみる！

<br><br>

## 🧩問題概要

整数 `N`が与えられたとき、

- 3 の倍数なら "`Fizz`"
- 5 の倍数なら "`Buzz`"
- 3 と 5 の両方の倍数なら "`FizzBuzz`"
- それ以外はそのまま `N` を出力
<br>

入力例：

    6

出力例：

    Fizz

<br>

https://paiza.jp/works/mondai/conditions_branch/conditions_branch__mod_boss

<br><br>

## ✅OKパターン①：シンプルなif文
```js
const rl = require('readline').createInterface({input:process.stdin});

rl.once('line',(input) => {
    const N = Number(input);
    
    if(N % 3 === 0 && N % 5 === 0){
        console.log("FizzBuzz");
    }
    
    else if (N % 3 === 0){
        console.log("Fizz");
    }
    
    else if (N % 5 === 0){
        console.log("Buzz");
    }
    
    else{
        console.log(N);
    }
        
    rl.close();

});
```
💡ポイント：複数条件が重なる場合は、一番厳しい条件を先に書く！

<br><br>

## ✅OKパターン②：文字列を連結するスタイル
```js
let result = '';
if (N % 3 === 0) result += 'Fizz';
if (N % 5 === 0) result += 'Buzz';
console.log(result || N);
```
🔹 メリット：コードが短く、冗長なif-elseが不要

<br><br>

## ✅OKパターン③：関数化して再利用しやすく
```js
function fizzBuzz(n) {
    if (n % 3 === 0 && n % 5 === 0) return "FizzBuzz";
    if (n % 3 === 0) return "Fizz";
    if (n % 5 === 0) return "Buzz";
    return n;
}

console.log(fizzBuzz(N));
```
🔹 メリット：他の問題でも使えるように、再利用可能なコードに
🔹 テストや別ロジックにも使えるので拡張性バツグン！

<br><br>

## ✅OKパターン④：三項演算子で1行にギュッと
```js
console.log(
  N % 15 === 0 ? "FizzBuzz" :
  N % 3 === 0 ? "Fizz" :
  N % 5 === 0 ? "Buzz" :
  N
);
```
🔹 メリット：コード1行で超スッキリ
🔹 デメリット：ネストが深いと読みづらくなるかも

<br><br>

## ✅OKパターン⑤：マップ（オブジェクト）活用で拡張しやすく
```js
function fizzBuzz(n) {
    let result = '';
    const rules = {
        3: 'Fizz',
        5: 'Buzz',
    };

    for (let key in rules) {
        if (n % Number(key) === 0) {
            result += rules[key];
        }
    }

    return result || n;
}
console.log(fizzBuzz(N));
```
🔹 メリット：7ならHoge、11ならFooとか簡単に追加できる！
🔹 柔軟性を重視！

<br><br><br>

## 📝気づきメモ
- `if-else`は条件の順序を絶対に意識する
- シンプルな問題でも、複数の正解パターンがある
- 書き方によって、可読性や拡張性が全然違う！
<br>

### ✨新しく学んだこと
- %（剰余演算子）を活用して条件をコントロールできる
- `||` を使った省略テク：`console.log(result || N)` で簡潔
- コードを関数化すると再利用性がUPする
- オブジェクト（マップ）による条件管理は拡張に最適
- ネストが深くなりすぎないよう、可読性を保つ意識が大事！

### 🎯まとめ

PaizaのFizzBuzz問題は「ただの3と5の話」で終わらず、分岐の考え方そのものを学べる最高の教材だった！

<br><br><br>[僕の失敗談(´;ω;｀)と解決法🐈](https://paizabeginner.wordpress.com/2025/05/27/paiza%e3%81%a7%e5%9f%ba%e6%9c%ac%e3%83%9e%e3%82%b9%e3%82%bf%e3%83%bc%ef%bc%9afizzbuzz%e5%95%8f%e9%a1%8c-%e3%81%84%e3%82%8d%e3%82%93%e3%81%aa%e8%a7%a3%e3%81%8d%e6%96%b9/)
