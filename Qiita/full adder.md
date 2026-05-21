# 全加算器

今回は、前回の続きで、論理演算を使って全加算器をJavaScriptで組んだ話！

## <br>問題概要
    入力：A, B（1桁のビット）, C1（前の桁からの繰り上がり）

    出力：C2（次の桁への繰り上がり）, S（この桁の合計）

```
入力：
1 1 1 →
    
出力：
1 1
```
<br>

https://paiza.jp/works/mondai/logical_operation/logical_operation__basic_step9

## <br>コード例：全加算器を論理演算でつくる
```js
const rl = require('readline').createInterface({ input: process.stdin });

rl.on('line', (input) => {
    // 入力を数値に変換：A と B は足し算対象、C1 は前の桁からの繰り上がり
    const [A, B, C1] = input.split(' ').map(Number);


    // 半加算器その1：A + B を計算
    const Cx = A & B;       // AとBが両方1なら繰り上がり発生（Carry）
    const Sy = A ^ B;       // AとBの合計（Sum）


    // 半加算器その2：Sy + C1 を計算（前の桁からの繰り上がりを足す）
    const Cy = Sy & C1;     // Sumと繰り上がりが両方1ならさらに繰り上がる
    const S =  Sy ^ C1;     // 最終的な合計（2けた目）


    // 最終的な繰り上がり（C2）：2つの繰り上がりをまとめる
    const C2 = Cx | Cy;     // どちらかに繰り上がりがあればOK（ORのほうが安全）


    // 結果を出力：次の桁への繰り上がりC2、現在の桁の合計S
    console.log(C2, S);

    rl.close();
});
```

- `A & B` は両方 1 のときのみ 1 になる → 最初のCarry ( `Cx` )
- `A ^ B` は A と B が異なるとき 1 になる → 中間のSum ( `Sy` )
- `Sy & C1` は中間 Sum と C1 が両方 1 なら繰り上がる → 追加Carry ( `Cy` )
- `Sy ^ C1` は合計 → 最終の `S`（1桁の合計）
- `Cx | Cy` は両方どちらかで繰り上がりが出れば 1 → 最終Carry ( `C2` )


### <br>解説

- `&`（AND）で「繰り上がりがあるか」を判定
- `^`（XOR）で「1桁目の合計を算出

これを2段階に分ければ、**全加算器** が完成！
<br>

計算式で書くと：

Sum = A ⊕ B ⊕ C1
Carry = (A & B) | ((A ⊕ B) & C1)

→ ⊕はJavaScriptだと `^`
```js
const Sum = A ^ B ^ C1;
const Carry = (A & B) | ((A ^ B) & C1);

console.log(Carry, Sum);
```

## <br>まとめ

- 全加算器は半加算器×2＋ORでできる
- `&`  `^`  `|` でロジック回路が作れて楽しい
- コメントつける理解が進む



<br><br>[📘 僕の失敗談と解決話！](https://paizabeginner.wordpress.com/2025/05/01/paiza%e3%81%a7%e5%9f%ba%e6%9c%ac%e3%83%9e%e3%82%b9%e3%82%bf%e3%83%bc%ef%bc%9a%e5%85%a8%e5%8a%a0%e7%ae%97%e5%99%a8/)
