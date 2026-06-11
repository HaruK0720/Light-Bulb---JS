# 要素の挿入　spliceの使い方

今回挑戦したのは【指定位置に要素を挿入する】という、配列操作の基本中の基本！


## <br>🎯問題概要

- 1行目で「N, M, K」が与えられる（配列の長さ、挿入位置、挿入したい値）

- 2行目にN個の整数が並ぶ配列が与えられる

- この配列の「M番目」に「K」を挿入し、1要素ずつ改行で出力せよ
<br>

入力例:

    5 3 10
    1 2 3 4 5

出力例:

    1
    2
    10
    3
    4
    5
<br>

https://paiza.jp/works/mondai/array_primer/array_primer__elm_insert


## <br><br>🛠️解き方

配列に挿入するには `splice()` を使うのがベスト！
```
配列.splice(挿入位置index, 削除数, 挿入したい値);
```

今回は `M` 番目に `K` を入れたいので、インデックスは `M-1`、削除はなしで `0` にする。

## <br>✅OKコード例

```js
const rl = require('readline').createInterface({ input: process.stdin });
const lines = [];

rl.on('line', (input) => {
    lines.push(input);
});

rl.on('close', () => {
    const [N, M, K] = lines[0].split(' ').map(Number);
    const arr = lines[1].split(' ').map(Number);

    // M番目（インデックスM-1）にKを挿入
    arr.splice(M - 1, 0, K);

    // 各要素を改行区切りで出力
    arr.forEach(num => console.log(num));
});
```
<Br><br>

## 気づきメモ

- `splice` は `0` から始まるインデックスを意識しないとズレる。
- `push` や `unshift` では位置を指定できないのでこの問題には向かない。
- `splice` は「挿入・削除・置換」何でもできる！

<Br>

## 🆕新しく学んだこと：spliceの用法まとめ

![スクリーンショット 2025-05-18 091158.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4018208/2c6fdc63-59fc-4835-8e78-fdd3816ddf19.png)

⚠注意：spliceは元の配列を直接変更します！（非破壊じゃない）


<br><br><br>[僕の失敗談(´;ω;｀)と解決法🐈](https://paizabeginner.wordpress.com/%e8%a8%98%e4%ba%8b%e4%b8%80%e8%a6%a7/)
