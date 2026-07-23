# 10 進数から M 進数に変換


前回に引き続き、進数の変換問題！2進数へ変換するコードを応用して10進数から何進数にでも変換できるようにできた！

<br>

## 問題概要

- 10 進数で表された整数 N, M が与えられる。
- N を M 進数に変換して出力する。

<br>

入力例：

    10 2

出力例：

    1010

<br>

https://paiza.jp/works/mondai/loop_problems2/loop_problems2__conv_nbase

<br><br><br>

## ✅OK例１：
```js
const rl = require('readline').createInterface({input:process.stdin});


rl.once('line', (input) => {
    const [N, M] = input.split(' ').map(Number);
    
    
    const base = [];
    for(let temp = N; temp > 0; temp = Math.floor(temp / M)){
        base.push(temp % M);
    }
    
    console.log(base.reverse().join(''));
    
    rl.close();
});
```
→前回のコードを応用（２→ M）

<br><br>

## ✅OK例２：
```js
const rl = require('readline').createInterface({input:process.stdin});


rl.once('line', (input) => {
    const [N, M] = input.split(' ').map(Number);
    
    console.log(N.toString(M));
    
    
    rl.close();
});
```
→`.toString(進数)` で、その進数の文字列へ変換。

<br><br>

## 📝気づきメモ

- M進数でも、２進数へ変換するときと同じで、
✅ Mで割り続ける
✅ 余りを記録する
✅ 逆順に並べる

　という方法で変換できるとわかった。

- `.toString(radix)`で変換するのがすごい楽だった。

<br>

## まとめ
進数変換は最初難しそうに見えるけど、変換方法がわかれば、そこまで難しいコードではない。あと、魔法の`.toString()` を使ってしまえばいい！



<br><br><br>[僕の失敗談(´;ω;｀)と解決法🐈](https://paizabeginner.wordpress.com/2025/06/06/paiza%e3%81%a7%e5%9f%ba%e6%9c%ac%e3%83%9e%e3%82%b9%e3%82%bf%e3%83%bc%ef%bc%9a10-%e9%80%b2%e6%95%b0%e3%81%8b%e3%82%89-m-%e9%80%b2%e6%95%b0%e3%81%ab%e5%a4%89%e6%8f%9b/)
