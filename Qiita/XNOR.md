# XNOR 演算の基本 !(A ^ B)

Paizaの論理演算シリーズ、今回は「XNOR」演算！

## <br>🎯 問題とステップ：

0 または 1 の整数 A, B が与えられる。A XNOR B の結果を出力せよ。

要は、AとBが同じなら1、違ったら0を出力する。

<br>

https://paiza.jp/works/mondai/logical_operation/logical_operation__basic_step7

## <br>✅コード例
```js
const [A, B] = require('fs').readFileSync('/dev/stdin', 'utf8').trim().split(' ').map(Number);

// 方法1：AとBが等しいかで判断
console.log(A === B ? 1 : 0);
```


```js
//方法2:ビット演算
const xnor = Number(!(A ^ B)); // XORの否定がXNOR！
console.log(xnor);
```

どっちも「AとBが同じなら1」を表現してるだけ。
でも 個人的には `===` のほうが分かりやすくて好き。

## <br>🔍 まとめ・補足ポイント
- `!(A ^ B)` だけだと true/false型になる → `Number()` で数値に変換！
- `^` はビットXOR → 違うときだけ`1`になる
- XNORはその逆：同じときだけ`1` → `!(A ^ B)` で表現可能

<br><br>[🐻僕の失敗談と解決話！🐈](https://paizabeginner.wordpress.com/2025/04/29/paiza%e3%81%a7%e5%9f%ba%e6%9c%ac%e3%83%9e%e3%82%b9%e3%82%bf%e3%83%bc%ef%bc%9axnor-%e6%bc%94%e7%ae%97%e3%81%ae%e5%9f%ba%e6%9c%ac-a-b/)
