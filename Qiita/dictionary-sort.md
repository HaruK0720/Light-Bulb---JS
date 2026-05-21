# Map の辞書順ソートでハマらない方法

Paizaの問題を解いていたら、「攻撃された人のダメージを記録し、名前の辞書順で出力せよ！」という指示に見事にハマった。`Map` は順番を保持しないので、そのまま `forEach()` すると順番が崩壊する！辞書順って何！？ `Map` にソート機能がない！？試行錯誤の末、「キーを配列化してソートすればいい」 という学びを得たので、その知見をシェアする！

<br>**問題概要**
攻撃された人のダメージを記録し、名前の辞書順で出力。

入力例:
```
3　　　　　//n
PAIIZA
PAIZA
PAIIIZA
2　　　　　//m
PAIIZA 2
PAIIIZA 3
```
出力例:
```
3
2
0
```


<br><br><br>**NG例**: Map に頼りすぎたコード
```js
const damageMap = new Map();
for (let i = 1; i <= n; i++) {
    damageMap.set(lines[i], 0);
}
for (let i = n + 2; i < n + 2 + m; i++) {
    let [person, damage] = lines[i].split(" ");
    damageMap.set(person, damageMap.get(person) + Number(damage));
}
damageMap.forEach((value, key) => console.log(value)); // 辞書順にならない！
```
ミスのポイント
✅ Map の挿入順に保証されている（辞書順にならない）

<br><br>**OK例1**: `Array.from()` でソート
```js
const sortedNames = Array.from(damageMap.keys()).sort();
sortedNames.forEach(name => console.log(damageMap.get(name)));
```
✅ Array.from() でキーを取り出し、sort() で辞書順ソート
✅ get() を使い、順番に出力


<Br><br>**OK例2**: `slice()` で無駄を省く
```js
const sortedNames = lines.slice(1, n + 1).sort();
sortedNames.forEach(name => console.log(damageMap.get(name)));
```
✅ すでに lines に名前があるので Map.keys() 取得不要
✅ キーアクセス回数が減り、わずかにパフォーマンス向上

<Br><br>**まとめ**
Map は順序を保証しない！辞書順ソートが必要なら、

・Array.from(damageMap.keys()).sort()
・もともとのリストを slice().sort() で利用

これで Map の罠にはまらない！

[僕の失敗談と解決話！](https://paizabeginner.wordpress.com/2025/03/14/paiza%e3%81%a7%e5%9f%ba%e6%9c%ac%e3%83%9e%e3%82%b9%e3%82%bf%e3%83%bc%e5%90%8d%e5%89%8d%e9%a0%86%e3%81%ab%e3%83%80%e3%83%a1%e3%83%bc%e3%82%b8%e3%82%92%e8%a1%a8%e7%a4%ba%e3%81%9b%e3%82%88%ef%bc%81map/)
