# forループ vs Map！検索を最適化する方法（辞書の基本問題）

Paizaの問題で学んだことをメモ。名前から財産を検索するだけのシンプルな問題だけど、「for ループと Map どっちが速い？」って考えたら、結構面白かった。

<br>📌 **問題概要**
n人の名前と財産を入力し、指定された人(S)の財産を出力する

入力例：
```
2　　　　　　　　//n
Kirishima 1
Kyoko 2
Kirishima　　　//S
```
出力例：
```
1
```
やること：
n 人の「名前＋財産」を受け取る
S（検索する名前）の財産を出力

<br><br>📝 forループで検索
```js
for (let count = 1; count <= N; count++){
    let pair = lines[count].split(" ");
    if(pair[0] === S){
        console.log(pair[1]); 
        break; // 見つけたら即終了！
    }
}
```
✅ シンプルで、少量データならOK
⚠️ O(N) なので、データが増えると遅くなる

<br><br>🚀 Map で最適化
```js
const dict = new Map();
for (let count = 1; count <= N; count++) {
    let [key, value] = lines[count].split(" ");
    dict.set(key, Number(value));
}
console.log(dict.get(S)); // O(1) で即検索！
```
✅ O(1) で高速検索
✅ ループ不要でシンプル

<br><br>🔍 **結論**
✅ 少量データなら for ループでOK
✅ 大量データなら Map で爆速検索！
適材適所でデータ構造を選ぶのが大事！
今回の問題のテーマが辞書の基本だったから、`map`の方で練習した方が良いかも。

[僕の失敗談と解決話！ 🚀](https://paizabeginner.wordpress.com/2025/03/12/paiza%e3%81%a7%e5%9f%ba%e6%9c%ac%e3%83%9e%e3%82%b9%e3%82%bf%e3%83%bc%e8%be%9e%e6%9b%b8%e3%81%ae%e5%9f%ba%e6%9c%ac%e5%95%8f%e9%a1%8c%ef%bc%81%e9%85%8d%e5%88%97%e6%a4%9c%e7%b4%a2-vs-map%e3%80%81/)
