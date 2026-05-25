# 文字列処理：日時分解　　おまけ：イベントリスナー

今回は文字列処理の日時データの変換問題を解いたから解説！
おまけで今回はイベントリスナーについて勉強してみた！

🔍問題概要

`yyyy/MM/dd hh:mm` の形式で与えられる日時を、以下の順で出力

入力される値：
```
yyyy/MM/dd hh:mm
```
期待する出力：
```
yyyy        
MM      
dd      
hh      
mm
```

https://paiza.jp/works/mondai/string_primer/advance_step3

## <br>💻コード例

```js
const rl = require('readline').createInterface({ input: process.stdin });

rl.on('line', (input) => {
    const parts = input.split(' ');      
    const date = parts[0].split("/");       
    const time = parts[1].split(':');     

    [...date, ...time].forEach(val => console.log(val));

    rl.close();
});
```

### ✏簡単に解説

- 入力を空白で2つに分ける → `date` と `time`

- それぞれ `/` と `:` でさらに分解
- スプレッド構文で日付と時間の配列を結合し、1つの配列にまとめて、 `console.log` で出力

<br><br><br>
# おまけ：イベントリスナーについて

今回のように、標準入力が 1行だけで完結しているケースでは `once` の方がベスト。
```js
rl.once('line', (input) => {
  const [date, time] = input.split(' ');

  [...date.split('/'), ...time.split(':')].forEach(val => console.log(val));
  
  rl.close();
});
```

## <br>✅ rl.once('line', ...) を使うとスマートな理由

### 🔍 .on()と.once()の違いまとめ
![スクリーンショット 2025-05-01 142630.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4018208/2844241c-ee40-4b76-9c61-d04fa4b0bcdd.png)



### ✅ .once()がスマートな理由

- `.on()` でも `removeListener` / `off` でリスナー削除可能だが、`.once()` は自動削除でシンプル。

- `.close()` は1回実行後にすぐ呼び出すのが自然で、タイミングが明確。
- 「1回だけ」の意図がコードで読みやすい。

※ `.once` は `on` + `removeListener` を1行で実現。

## <br>🛠 JavaScriptのイベントリスナーってなに？

イベントリスナーって、ざっくり言えば、

「イベントが起きたときに動く関数を登録する仕組み」。


### <br>🔁 readline の例で見るイベントリスナー

Node.js の `readline` モジュールでも、同じ仕組みが使われている：

```js
rl.on('line', (input) => {
    // ユーザーが1行入力するたびにこの関数が実行される
    console.log(`入力：${input}`);
});
```
この `on('line', callback)` は
👉 「ユーザーが1行入力したら `callback` を呼んでね！」という イベントリスナーの登録！

### <br>💡 重要なポイント

イベントリスナーとは？： イベントが起きたときに実行される関数を登録する仕組み

例： `click` , `load` , `line` , `data` , `error` , `close` など

目的： イベント駆動型のプログラムを作る（待ち構えて反応する）

## <br>.addEventListener （ブラウザ向け、HTML・DOM）

どこで使う？
ブラウザ上で、ボタンやフォーム、画面の要素に対して使う。
```js
 element.addEventListener('click', () => {
     console.log('クリックされた！');
 });
```
特徴:

- 同じイベントに複数個リスナーを登録できる
- 登録したイベントをあとで削除（`remove`）できる
- ブラウザの標準的なイベントリスナーの登録方法

## <br>.on （Node.js 向け、サーバー・バックエンド）

どこで使う？
Node.jsで、`readline`、httpサーバー、ファイル操作などのイベントを持つオブジェクトに対して使う。
```js
server.on('request', (req, res) => {
    res.end('Hello World');
});

rl.on('line', (input) => {
    console.log('ユーザーが入力した:', input);
});
```
特徴:
- イベントドリブン（＝イベントが起きたら動く）なプログラムを作る
- `.on()` と `.once()` はどちらも `EventEmitter` の標準メソッドで、用途に応じて使い分ける

## <br>イベントリスナーの基本：

✅ ブラウザでは、DOM要素（例: ボタンやフォーム）のイベントを扱うために `.addEventListener` を使用する。


✅ Node.jsでは、EventEmitterベースのイベント（例: 入力やサーバーリクエスト）を扱うために `.on` や `.once` を使用する。
<br>

ただし、Node.jsでも puppeteer（ヘッドレスブラウザ）や jsdom（仮想DOM環境）のようなDOM互換環境では`.addEventListener` が使われる場合がある。

用途に応じて適切なメソッドを選ぼう！

<br>

![スクリーンショット 2025-05-01 142750.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4018208/e0c46f45-3545-48cb-8dde-7d4a0928c76c.png)

補足: 両者とも複数リスナー登録可能。`.once()`は自動削除で管理が楽。


<br><br>[僕の失敗談(´;ω;｀)と解決法🐈](https://paizabeginner.wordpress.com/about/)
