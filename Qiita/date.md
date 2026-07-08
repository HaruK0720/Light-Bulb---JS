# 曜日判定 Date

今日もPaizaの条件分岐 – 曜日判定にチャレンジ！

<Br>

## 🧩 問題概要

問題はシンプル、「1日は日曜日。X日は何曜日か？」。


入力例:

    11

出力例:

    Wed
<br>

https://paiza.jp/works/mondai/conditions_branch/conditions_branch__mod_step4

<Br><br><br>

## ✅コード例：条件武器で解く
```js
const rl = require('readline').createInterface({ input: process.stdin });

rl.once('line', (input) => {
    const X = Number(input);
    const day = (X - 1) % 7;

    if (day === 0) console.log("Sun");
    else if (day === 1) console.log("Mon");
    else if (day === 2) console.log("Tue");
    else if (day === 3) console.log("Wed");
    else if (day === 4) console.log("Thu");
    else if (day === 5) console.log("Fri");
    else if (day === 6) console.log("Sat");

    rl.close();
});
```

<br><br><br>

## ✅コード例２：配列
```js
const rl = require('readline').createInterface({input:process.stdin});


rl.once('line',(input) => {
    const X = Number(input);
    
    const week = ["Sat", "Sun", "Mon", "Tue", "Wed", "Thu", "Fri"];
    
    console.log(week[X % 7]);
    
    rl.close();
});
```
- 1 日は日曜日ということから、7で割ったときに１余る日が日曜日として曜日の配列を作成。
- インデックスでアクセスして曜日を取得。

<br><br>

## 🔍 気づきメモ

- 1日は日曜日→つまり `X = 1` のとき "`Sun`" を返すように余りと曜日を配列に。
- `X % 7` の結果に対応するように、配列の 0 番目は”`Sat`”にする必要がある。
- `if`文で全部書くより、データをうまく構造化（今回なら配列）する方がスマート。

<br><br>

## 📣 まとめ
「曜日の判定って、ただの7通り」だけど、条件分岐以外にも解き方があって、勉強になった！

<br><br><br>[僕の失敗談(´;ω;｀)と解決法🐈](https://paizabeginner.wordpress.com/2025/05/26/paiza%e3%81%a7%e5%9f%ba%e6%9c%ac%e3%83%9e%e3%82%b9%e3%82%bf%e3%83%bc%ef%bc%9a%e6%9b%9c%e6%97%a5%e5%88%a4%e5%ae%9a-date/)

<br><br><br>

### 💡おまけ

年月日が入力され、その曜日を出力する問題だった場合を考えてみる。

### ✅ コード：年月日を入力して曜日を出力
```js
// 標準入力の読み取り設定
const readline = require('readline');
const rl = readline.createInterface({ input: process.stdin });

// 入力を1行だけ読み取る
rl.on('line', (input) => {
    // 入力を空白で分割し、数値に変換（例：2025 5 23）
    const [year, month, day] = input.split(' ').map(Number);

    // 月は0始まりのため、1引く（JavaScriptの仕様）
    const date = new Date(year, month - 1, day);

    // 曜日の配列（getDay()の戻り値に対応）
    const week = ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat'];

    // 曜日インデックスを取得し、対応する文字列を出力
    console.log(week[date.getDay()]);

    rl.close();
});
```
- `Date` オブジェクトを使うことで、指定した日付の曜日やその他の情報を取得できるようになる。
- JavaScript の `Date` では月（month）は 0 始まり（1月が 0、12月が 11）なので `month - 1` が必要。
- `getDay()` は曜日インデックス（ 0 : 日曜 〜 6 : 土曜）を返す
- そのインデックスをもとに `week` 配列から文字で出力

<br><br>

![スクリーンショット 2025-05-24 214215.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4018208/5c86d4f0-4749-40ec-9ff7-a5c152cd1d35.png)


