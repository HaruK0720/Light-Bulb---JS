# 論理積( AND )の基本 &

AND演算の使い分けについて技術だけ抜き出してまとめてみた！



## <br>問題概要

0 または 1 の整数 A と B が与えられます。 A AND B の結果を出力してください。

<br>入力例：
```
0 1
```
出力例：
```
0
```
<br>

https://paiza.jp/works/mondai/logical_operation/logical_operation__basic_step1


## <br> ❌ NGコード
```js
if (A === 1 && B === 1) {
  console.log(1);
} else {
  console.log(0);
}
```
今回の問題では条件分岐を使わないのが条件。
(`&&` はブール判定用なので、「真偽値」を返す式)


## <br>✅ OKコード
```js
const [A, B] = input.split(' ').map(Number);
console.log(A & B);
```
`&` は「ビットAND」。`1 & 1` → `1`、それ以外 → `0`

## <br>💡 技術メモ
- `&`：整数同士のビット演算（論理積）
- `&&`：ブール値の論理演算（短絡評価）
- `if`文より論理演算子で一発解決のほうがコードがスッキリ
- `x & 1 === 0` で偶数判定にも使える


### <br>📘 新しく学んだことまとめ
- `a & b` でビット単位のANDが可能
- `&` vs `&&`、用途に応じて使い分け
- ビット演算はフラグ管理や高速な条件判定に便利



<br><br>[僕の失敗談と解決話！](https://paizabeginner.wordpress.com/2025/04/23/paiza%e3%81%a7%e5%9f%ba%e6%9c%ac%e3%83%9e%e3%82%b9%e3%82%bf%e3%83%bc-%e8%ab%96%e7%90%86%e7%a9%8d-and-%e3%81%ae%e5%9f%ba%e6%9c%ac%e3%80%80/)


