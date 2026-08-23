# 文字列の抽出　RegExp・matchAll


今回のpaizaの問題は「タグで囲まれた部分の文字を取り出せ」という問題。

はじめは `split` とかでいけないかな？と思って始めたけど、やっぱり正規表現が便利！

でも見慣れないうちは、使うの避けちゃうよね(^▽^)/

<br><br>

# 問題概要

- ある長さ `N` の文字列の中から

- `<start>` と `<end>` で囲まれた部分をすべて抽出する

- 中身が空なら `<blank>` を出力

<br>

入力例：

    <abc> <xyz>
    hoge<abc>piyo<xyz>

出力例：

    piyo

<br>

https://paiza.jp/works/mondai/c_rank_skillcheck_archive/extract_word_00

<br><br><br>

# ❌NG例
```js
const regex = new RegExp(/${start}(.*?)${end}/g); // ❌
```
## なぜダメ？

`/.../` の中では `${}` が展開されない！
実際には `/${start}(.*?)${end}/g` という文字そのものが評価されてしまう。

結論：変数を使うならテンプレートリテラル（バッククォート）必須！

<br><br><br>

# ✅OK例
```js
const rl = require('readline').createInterface({input:process.stdin});

const lines = [];

rl.on('line', (input) => {
    lines.push(input);
});

rl.on('close', () => {
    const [start, end] = lines[0].split(' ');
    const N = lines[1];
    
    const regex = new RegExp(`${start}(.*?)${end}`, 'g');
    
    const match = [...N.matchAll(regex)];
    
    for(const text of match){
        console.log(text[1] !== '' ? text[1] : '');
    }
});
```

<br><br>  

## 💡解説ポイント

### ①RegExpとは? なぜ“なのか？　

「正規表現」とは英語で Regular Expression のことで、略して RegExp と呼ばれる。

<br>

💡`/…/` の中に変数をそのまま埋め込めないので、テンプレートリテラル（``）を使う

<br>

```js
✅const regex = new RegExp(`${start}(.*?)${end}`, 'g');
❌const regex = new RegExp(/${start}(.*?)${end}/g);
```

<br>

### ②’g’とは？

`g` は正規表現のフラグ。

フラグとは？
フラグは、正規表現の検索の方法や範囲を変更する。

`g`（グローバル）：すべてのマッチを検索（デフォルトでは最初のマッチのみ）。

💡このコードで `matchAll` がすべての `start` と `end` のペアを見つけるために必要！

※

- リテラル形式 `/abc/g` は、正規表現とフラグを直接記述できる特殊な構文なので、ここではクォートは不要。
- 一方、RegExpコンストラクタはパターンとフラグを文字列として受け取るため、文字列形式で指定する必要がある。

<br>

### ③matchAll とは？　なぜスプレッド構文なのか？

`matchAll()` は文字列メソッドで、正規表現にマッチしたすべての結果をイテレータ（反復処理可能なオブジェクト）で返すメソッド。

これにより、複数マッチの詳細（キャプチャグループ含む）を簡単に取得できる！

<br>

タグごとテキストを抽出するマッチ全体（①）があるから、タグに囲まれた「テキスト」のみ抽出するキャプチャ部分（②）がある。

<br>

戻り値はイテレータなので、そのままだと配列ではない。

そこで、`[…N.matchAll(regex)]` とスプレッド構文を使ってイテレータを配列に展開した！

<br>

例:
```js
const str = 'a1b2c3';
const regex = /\d/g;

const matches = [...str.matchAll(regex)];
console.log(matches);


// [
//   ["1", index: 1, input: "a1b2c3", groups: undefined],
//   ["2", index: 3, input: "a1b2c3", groups: undefined],
//   ["3", index: 5, input: "a1b2c3", groups: undefined]
// ]
```

配列にすると `for…of` や `forEach` で簡単にループできるようになる。

※補足：
`matchAll()` は `RegExp` に `g` フラグが必須。
なければ TypeError が発生。

<br>

### ④text [1] となる理由　キャプチャとは？　

正規表現の `()` は 「キャプチャグループ」 と呼ばれ、マッチした部分文字列を「グループ」として取り出せる。

`matchAll` や `match` の戻り値は、配列の0番目が「マッチ全体」、1番目以降がキャプチャグループに対応している。

<br>

例:
```js
正規表現: /foo(ba)r/
文字列: "foobar"
マッチ結果は:

[
  "foobar",   // 0番目：マッチ全体
  "ba",       // 1番目：1つ目のキャプチャグループ ( ) にマッチした部分
  index: 0,
  input: "foobar",
  groups: undefined
]
````
  

つまり、今回のコードのtext`[1]`は、開始タグと終了タグの間にあった「中身の文字列」を指している。

<br>

### ⑤(.*?) とは？

- `.` ： 任意の1文字。

- `*`：0回以上の繰り返し。

- `?` ：非貪欲…可能な限り短い範囲でマッチ・最小マッチ

つまり`(.*?)` は「任意の文字が0回以上続く部分をキャプチャするが、可能な限り短い範囲でマッチする」というパターン。

<br><br><br>

## 📘新しく学んだことメモ ＆ まとめ

- RegExpコンストラクタに変数を入れるときはテンプレートリテラル `` を使う
- `g` フラグは 全マッチ探索するために必要（`matchAll`に必須！）
- `(.*?)` は「できるだけ短くマッチする非貪欲キャプチャ」
- `matchAll()` の戻り値は イテレータ。配列に変換してからループ！（スプレッド構文）



<br><br><br>[僕の失敗談(´;ω;｀)と解決法🐈](https://paizabeginner.wordpress.com/about/)
