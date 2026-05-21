# .sort()でハマらない方法：Set×BigIntは比較関数必須！

Paizaの`Set`問題で、数値が昇順にならないバグに直面しました。原因は `.sort()` の仕様と `BigInt` の特性にあった！

## <br>🧪 問題の概要
2つの数列`A`, `B`与えられ、それぞれの値を重複なく昇順で出力せよ。

<br>入力例:
```
3
1 2 3
3 4 5
```
出力例:
```
1 2 3 4 5
```
<br>

https://paiza.jp/works/mondai/data_structure/data_structure__set_boss



## <br>💥 NGコード：文字列としてソートされる罠
```js
const arrA = lines[1].split(' ');
const arrB = lines[2].split(' ');
const seen = new Set([...arrA, ...arrB]);
console.log([...seen].sort().join(' '));
```
→ 出力が `10 2 3` みたいに崩壊。

なぜ？→ `.sort()` のデフォルトは文字列ソートだから。

## <br>✅ OKコード：BigInt＋比較関数
```js
const arrA = lines[1].split(' ').map(BigInt);
const arrB = lines[2].split(' ').map(BigInt);
const seen = new Set([...arrA, ...arrB]);

const sorted = [...seen].sort((a, b) => (a < b ? -1 : a > b ? 1 : 0));
console.log(sorted.join(' '));
```

### ✔ 解説
✅`BigInt`型で巨大な数にも対応

✅`.sort()` に比較関数が必須（デフォは文字列比較）

✅`a - b` はNG → `BigInt - BigInt = BigInt` なので戻り値が 、
　 `Number` じゃなくて型エラー

## <br>📌 技術メモ

- `new Set([...])` は重複除去に便利
- `.sort()` は数値比較を明示しないとバグる
- `BigInt` 使うなら `map(BigInt)` + 比較関数必須


<br><br>[僕の失敗談と解決話！](https://paizabeginner.wordpress.com/2025/04/22/paiza%e3%81%a7%e5%9f%ba%e6%9c%ac%e3%83%9e%e3%82%b9%e3%82%bf%e3%83%bc-setxbigint%e3%81%a7%e3%82%bd%e3%83%bc%e3%83%88%e3%81%8c%e3%83%90%e3%82%b0%e3%82%8b%e7%90%86%e7%94%b1/)
