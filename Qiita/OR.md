# 論理和( OR )の基本 |

今回はPaizaの「OR演算」問題で、条件分岐を封印して論理和をスマートに書く方法を学んだ！

## <br>🧩 問題概要
入力で 0 または 1 の整数 A, B が与えられます。
「A OR B」の結果を出力せよ、という内容。

例）
入力: `0 1` → 出力: `1`
入力: `1 1` → 出力: `1`

「OR（論理和）」は、どっちかが 1 なら 1 を返すルール。
<br>
https://paiza.jp/works/mondai/logical_operation/logical_operation__basic_step2

## <br>🙅‍♂️ NGコード
```js
if (A === 1 || B === 1) {
  console.log(1);
} else {
  console.log(0);
}
```

## <br>✅ OKコード
```js
const [A, B] = input.split(' ');
console.log(A | B);
```
ビットOR演算子 `|` を使えば、条件分岐なしで「論理和」がそのまま表現できる。
<br>
<br>
```js
0 | 0 → 0

0 | 1 → 1

1 | 0 → 1

1 | 1 → 1
```

## <br>💡 ポイントまとめ
- `|` はビット演算子、論理和に使える
- `||`（論理演算子）と混同しないこと！
- `if`文を使わずスッキリ処理 → 可読性UP
- 入力が 0/1 に限定されてる場合は積極的に使いたい



<br><br>[僕の失敗談と解決話！](https://paizabeginner.wordpress.com/2025/04/24/paiza%e3%81%a7%e5%9f%ba%e6%9c%ac%e3%83%9e%e3%82%b9%e3%82%bf%e3%83%bc%ef%bc%9a%e8%ab%96%e7%90%86%e5%92%8c-or-%e3%81%ae%e5%9f%ba%e6%9c%ac/)
