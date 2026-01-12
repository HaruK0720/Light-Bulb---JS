# padStart() でゼロ埋めをスマートに！


 paiza のゼロ埋め問題に挑戦したら、最初は if 文ゴリ押しでダサいコードに…。`padStart()` を知ったら、一発で解決した ので、その学びをメモ。


<br>整数 n（0~999）が1つ入力されるので3桁にそろえて出力する処理 を考える。
入力例　→　9　45　123
出力例　→　009　045　123

<br>❌ NGコード：if 文でゴリ押し
```js
rl.on('line', (line) => {
    if (line.length === 3) {
        console.log(line);
    } else if (line.length === 2) {
        console.log("0" + line);
    } else {
        console.log("00" + line);
    }
    rl.close();
});
```
🚨 問題点
if の分岐が増えてコードが読みにくい
バグの原因になりやすい

<br>✅ OKコード：padStart() で一発解決！
```js
rl.question('', (line) => {
    console.log(line.padStart(3, '0'));
    rl.close();
});
```
✨ 改善ポイント
✅ padStart(3, '0') で たった1行で解決！
✅ rl.question() で 一回の入力を確実に処理！
✅ 可読性アップ＆ミス減少！

<br>📌 padStart() のポイント

不足分を指定の文字で埋める
```js
console.log('9'.padStart(3, '0'));  // "009"
console.log('42'.padStart(3, '0')); // "042"
```
デフォルトは半角スペース
```js
console.log('42'.padStart(5)); // "   42"
```
ターゲットの長さ以下なら何もしない
```js
console.log('1234'.padStart(3, '0')); // "1234"
```

<br>🔍 まとめ

最初は if 文ゴリ押しで書いてたけど、padStart() で一発解決！
「ゼロ埋め？ → padStart() でOK！」って流れを覚えよう！🔥

※ちなみに、on('line',～)は複数行入力向けと聞いたので、.questionを使ったのですが、
　paizaの問題で.question()を使うと上手く処理されず正解になりません(´;ω;｀)
　通過するためにon('line',～)の方を使いました。
 
[僕の失敗談と解決話！](https://paizabeginner.wordpress.com/2025/03/04/paiza%e3%81%a7%e5%9f%ba%e6%9c%ac%e3%83%9e%e3%82%b9%e3%82%bf%e3%83%bc-padstart%e3%81%a7%e3%80%810%e5%9f%8b%e3%82%81%e5%87%a6%e7%90%86%e3%82%92%e3%82%b9%e3%83%9e%e3%83%bc%e3%83%88%e3%81%ab%ef%bc%81/)

