# 辞書検索をスマート化する　Map.get() ?? -1

Paizaの「paiza商店の商品価格」問題を解いたときの学び💡
`Map`って、こんなに使いやすかったんだ…！

## <br>🧾 問題概要：paiza商店でお買い物

- N個の商品（名前と価格）が与えられる
- M個の商品名が書かれた「お買い物リスト」が与えられる
- 各商品について、商店にあれば価格を、なければ -1 を出力する

<br> 入力例:
```
3 4
eraser 50
pencil 30
book 100
book
eraser
pencil
margaret
```
出力例:
```
100
50
30
-1
```

<br>

https://paiza.jp/works/mondai/data_structure/data_structure__dict_step4


## <br>△NGかも例（注意）
```js
priceMap.set(productName, price); // ❌ 価格が文字列のまま
```
このままだと「計算したいとき」に困る！
例えば合計金額出すときに '100' + 50 で 150 じゃなくて 10050 になる（爆）
なので、ちゃんと `Number()` で数値変換が必要。
```js
priceMap.set(productName, Number(price)); // ⭕️安全！
```

## <br>✅?? を使った方がシンプル！
```js
priceMap.has(item) ? priceMap.get(item) : -1; // ⛔ 
priceMap.get(item) ?? -1;                     // ⭕ 短くて読みやすい
```

`.get()` は見つからないと `undefined` を返すから、`??` と組み合わせるだけでOK！


## <br>💻 コード全体（コメント付き）
```js
const rl = require("readline").createInterface({ input: process.stdin });
const lines = [];

// 標準入力を1行ずつ配列に格納
rl.on("line", (input) => {
  lines.push(input);
});

rl.on("close", () => {
  // 1行目: 商品数N、お買い物リスト数Mを数値に変換して取得
  const [N, M] = lines[0].split(" ").map(Number);

  // 商品名と価格を格納するMap（辞書）を作成
  const priceMap = new Map();

  // N個の商品をMapに登録（価格は数値に変換）
  for (let i = 1; i <= N; i++) {
    const [productName, price] = lines[i].split(" ");
    priceMap.set(productName, Number(price));
  }

  // お買い物リストの部分を取得（N+1行目〜末尾まで）
  const shoppingList = lines.slice(N + 1);

  // 各商品について、価格を取得（なければ -1）して配列に
  const results = shoppingList.map(item =>
    priceMap.get(item) ?? -1
  );

  // 結果をまとめて出力
  console.log(results.join('\n'));
});
```

### <br>🔍 技術メモ & まとめ
- `Map` はJSの辞書操作で適している。構文もシンプル。
- `.set()` 時に `Number(price)` を忘れるとバグのもと。
- `.has()` より `get() ??` の方がスッキリ書ける。
- 結果は `join('\n')` で一気に出力 → パフォーマンスも良き。

<br><br>  [僕の失敗談(´;ω;｀)と解決話！🚀](https://paizabeginner.wordpress.com/2025/04/19/paiza%e3%81%a7%e5%9f%ba%e6%9c%ac%e3%83%9e%e3%82%b9%e3%82%bf%e3%83%bc%ef%bc%9amap%e3%81%a7%e5%95%86%e5%93%81%e4%be%a1%e6%a0%bc%e3%82%92%e4%b8%80%e7%99%ba%e6%a4%9c%e7%b4%a2%ef%bc%81/)


