# 配列検索! 配列から最小 index を探す方法！

Paizaで「特定の財産額を持つ人を探す」問題に挑戦！でも .length で k を取得しようとしてズッコケ、Number() を忘れて比較エラー…。配列検索の基礎をガッツリ学んだのでシェアするよ！

<br>**問題概要**
1から n まで番号がついた人々の財産リスト a_1, ..., a_n がある。財産が k 円の人の番号を出力する。ただし、同じ k を持つ人が複数いた場合は 最も小さい番号を出力する。
```
n
a_1
...
a_n
k
```

<br>入力例
```
5　//n
3
7
5
7
2
7　// k
```
出力例
```
2
```


<br>**NG例**（今回やらかしたコード）
```js
const N = lines[0]; // ❌ Number()を忘れた
const k = Number(lines.length); // ❌ .length は配列の要素数！
for (count = 1; count <= N; count++) { // ❌ let なし
    if (lines[count] === k) { // ❌ 数値変換忘れ
        console.log(count);
        break;
    }
}
```

<br><br>**OK例**（修正コード）
```js
const N = Number(lines[0]);  // ✅ しっかり数値変換！
const k = Number(lines[N + 1]);  // ✅ k の正しい取得方法！
for (let count = 1; count <= N; count++) {
    if (Number(lines[count]) === k) {
        console.log(count);
        break;
    }
}
```

ミスしないためのポイント
✅ Number() を忘れると文字列比較になってバグる！
✅ for ループの let を忘れるとグローバル変数になってエラー！
✅ break; を使えば最初に見つけた k でループを抜けられて効率的！
✅ .length は配列の要素数であり、k の取得には関係ない！
   →配列の最後の要素を取りたいなら `lines[lines.length - 1]`を使うべき？

<br>**まとめ**
配列検索で「最初に見つけた位置」を出力するならインデックス記録が最適解！

🔹 フラグ vs インデックス記録：found フラグで判定する方法もあるけど、
　　この問題ではインデックス記録の方がシンプル！
  
🔹 forEach は break できない → for ループを使おう！


👉 [僕の失敗談と解決話！](https://paizabeginner.wordpress.com/2025/03/08/paiza%e3%81%a7%e5%9f%ba%e6%9c%ac%e3%83%9e%e3%82%b9%e3%82%bf%e3%83%bc-index%e5%8f%96%e5%be%97%e3%81%a8%e3%81%af%ef%bc%9fjs%e3%81%a7%e9%85%8d%e5%88%97%e6%a4%9c%e7%b4%a2%e3%81%ae%e5%9f%ba%e6%9c%ac/)
