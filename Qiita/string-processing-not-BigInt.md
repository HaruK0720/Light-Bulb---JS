# 巨大な数の足し算（文字列処理）　BigInt禁止でどうする!?

「`BigInt` 使えば一発でしょ」と思ったけど、今回は文字列処理の分野なので文字列処理で解いていく！

<br><Br>

## 📌 問題概要

1000桁までの2つの数字（文字列SとT）を足して、その結果を文字列で出力します。注意点は以下のとおり：

- SとTは文字列（数字のみ）
- 桁の長さは同じ
- 数値がめちゃくちゃ大きい


入力例：

    1029384756
    1029384756

出力例：

    2058769512


設計のカギは「下の桁から順に計算＋繰り上がり」

<Br>

https://paiza.jp/works/mondai/string_primer/advance_step11

<br><br>

## 💥これでも解けるけど　今回は文字列処理でやりたい
```js
const rl = require('readline').createInterface({ input: process.stdin });

const lines = [];

rl.on('line', (input) => {
    lines.push(input);
});

rl.on('close', () => {
    const [A, B] = lines.map(BigInt); // ここで変換！

    // BigInt同士で加算し、文字列として出力
    console.log((A + B).toString()); 

});
```

<br><br>

## 📌文字列処理バージョン

「繰り上がりあり」「非常に大きな桁の数字でも対応可」「BigInt非使用」

```js
const rl = require('readline').createInterface({ input: process.stdin });
const lines = [];

rl.on('line', (line) => lines.push(line));
rl.on('close', () => {
    let [s, t] = lines;

    // 桁数が同じであることが前提
    let ans = "";
    let carry = 0;

    // 下位の桁から計算する（末尾の文字からループ）
    for (let i = s.length - 1; i >= 0; i--) {

        const digitSum = Number(s[i]) + Number(t[i]) + carry; // 同じ桁の文字を数値に変換し、繰り上がりも加算

        carry = Math.floor(digitSum / 10); // 10以上なら繰り上がりが発生 → 次のループに持ち越す

        ans = String(digitSum % 10) + ans; // 現在の桁の値（1桁）を取り出し、先頭に追加（上の桁へつなげる）
    }


    // 最後に繰り上がりが残っていたら追加
    if (carry > 0) {
        ans = String(carry) + ans;
    }

    console.log(ans);
});
```
🔍 ポイント

- `for (let i = s.length – 1; i >= 0; i–)` で 末尾からループ。
- `digitSum % 10`  がその桁の数、 `Math.floor(digitSum / 10)`  が繰り上がり。
- 最後に `carry > 0` を忘れず確認。

### <Br>⚠️ 注意

このコードは `S` と `T` が同じ桁数 である前提。

違う長さの場合は短い方を `padStart` で補完すればOK！　

例：
```js
if (s.length < t.length) s = s.padStart(t.length, '0');
if (t.length < s.length) t = t.padStart(s.length, '0');
```

## <br>📝 気づきメモ

- 最後の繰り上がり処理、忘れやすいから注意。

- 足し算は下の桁から繰り上がりを考えて進めるから、左からじゃなく「右（下の桁）」から処理するのが大事！

- `padStart()`で桁をそろえれば応用も効く！

## <br>✨ まとめ

今回は「数値に変換しないで、文字列のまま足し算する」方法を学んだ。下の桁から繰り上がりを意識して処理することで、JavaScriptでも正確に大きな数を扱えるようになる！

<br><br><br>
[🐻僕の失敗談(´;ω;｀)と解決法🐈](https://paizabeginner.wordpress.com/about/)
