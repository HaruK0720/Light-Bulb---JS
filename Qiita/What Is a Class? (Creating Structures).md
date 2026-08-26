# クラスって何？（構造体の作成）


今回から少しレベルアップして、paizaのクラス・構造体メニューの問題に挑戦していく！

ちょうど、前回オブジェクトについて学んだことが役立つのか？

<br>

# 問題概要

- 生徒一人につき「名前 年齢 誕生日 出身地」が渡される。

- それを User クラスの形にまとめる。

- 出力はキレイに

```
User{
nickname : 名前
old : 年齢
birth : 誕生日
state : 出身地
}
```
の形にする。

<br>

入力例：

    3
    mako 13 08/08 nara
    megumi 14 11/02 saitama
    taisei 16 12/04 nagano

出力例：

    User{
    nickname : mako
    old : 13
    birth : 08/08
    state : nara
    }
    User{
    nickname : megumi
    old : 14
    birth : 11/02
    state : saitama
    }
    User{
    nickname : taisei
    old : 16
    birth : 12/04
    state : nagano
    }

<br>

https://paiza.jp/works/mondai/class_primer/class_primer__make

<br><br><br><br>

# ✅OK例：
```js
const rl = require('readline').createInterface({ input: process.stdin });
const lines = [];

rl.on('line', (input) => {
  lines.push(input);
});

rl.on('close', () => {
  const N = Number(lines[0]);

  class User {
    constructor(nickname, old, birth, state) {
      this.nickname = nickname;
      this.old = old;
      this.birth = birth;
      this.state = state;
    }

    format() {
      return `User{
nickname : ${this.nickname}
old : ${this.old}
birth : ${this.birth}
state : ${this.state}
}`;
    }
  }

  for (let i = 1; i <= N; i++) {
    const [nickname, old, birth, state] = lines[i].split(' ');
    const user = new User(nickname, old, birth, state);
    console.log(user.format());
  }
});
```
  

## まず、ざっくり説明すると…

- `User` という「設計図（ひな形）」を作っている
- その設計図をもとに、たとえば「まこさん」や「めぐみさん」といった実際のユーザー（インスタンス）を作る。
- それぞれのユーザーは、名前（nickname）や年齢（old）、誕生日（birth）、住んでいる場所（state）という情報を持っている。


- そして、そのユーザーの情報を決まった形で表示できるようにしている。

<br><br>

## コードの詳しい説明
```js
class User {
```
ここで「`User`（ユーザー）」というクラス（設計図）を作っている。

「クラス」は複数のデータをひとまとめにして管理しやすくするもの。

<br><br><br>

```js
 constructor(nickname, old, birth, state) {
```

「`constructor`（コンストラクタ）」は特別な関数で、`User`を作るときに呼ばれる。

作るときに「`nickname`」や「`old`」などの情報を渡して、それを`User`の中にしまう役割をする。

<br><br><br>

```js
    this.nickname = nickname;
    this.old = old;
    this.birth = birth;
    this.state = state;
```

`this` は「これから作る`User`オブジェクト自身」を指している。

`his.nickname` は「このUserのニックネーム」みたいに、その`User`が持つ情報を設定している。

つまり、「渡されたニックネームを、この`User` の `nickname` に保存する」という意味。

<br><br><br>

```js
  format() {
```

`format` は「この`User`の情報を文字列として返す関数」

この関数を呼ぶと、`User`の中の情報を見やすい形で表示できる文字列が返ってくる。


<br><br><br>

```js
    return `User{
nickname : ${this.nickname}
old : ${this.old}
birth : ${this.birth}
state : ${this.state}
}`;
```

ここはテンプレートリテラルと呼ばれる書き方で、

`this.nickname` など`User`の情報を一つずつ取り出して、決まったフォーマットの文字列を作っている。

こうすると問題で指定された表示になる。

<br><br><br><br><br><br>

# ✅ クラスとは？構造体と何が似てるの？

構造体（C言語などにある struct） は
→ 「複数の種類のデータをひとまとめにする入れ物」。
```c
例: struct Person { name, age, height }
```

クラス も
→ 「複数のデータをまとめる型」で、
さらに「データを操作する関数（メソッド）」も一緒に持てる。

つまり、「クラス ＝ 拡張された構造体」 と思えばOK！

<br>

- データ（プロパティ）
- 動作（メソッド）
をまとめて管理できるのがポイント！

<br><br><br>

# ✅ クラスの基本構文
```js
class クラス名 {
  constructor(引数1, 引数2, ...) {
    // this.プロパティ名 = 引数
  }

  メソッド名() {
    // 何かの動作
  }
}
```
- `class` キーワードでクラスを作る。

- `constructor` は作るときに呼ばれる特別な関数。

- `this` は「このクラスで作られた1つのオブジェクト自身」を指す。

<br><br><br>


## ✅ 情報のセットの仕方（constructor の役割）

例えばこの部分👇
```js
constructor(nickname, old, birth, state) {
  this.nickname = nickname;
  this.old = old;
  this.birth = birth;
  this.state = state;
}
```
`new クラス名(…) `で作ると、`constructor` が動く！
引数として渡した値を `this.プロパティ名` に代入する。
こうして、新しいオブジェクトにそれぞれのデータがセットされる。

<br>

例：
```js
const user = new User("mako", 13, "08/08", "nara");
```

この1行で「mako」というデータが中に入った `User` を作れる。

<br><br><br><br><br>

## ✅ 構造体（struct）は 値型

値型 とは：

- 変数に入れたら「実体そのもの」がコピーされる。
- 代入すると新しいコピーができる。
- コピー後に片方を変えても、もう片方には影響なし。

<br>

例（C言語で struct）：
```js
    struct Person p1 = { "Alice", 20 };
    struct Person p2 = p1; // p1の値を丸ごとコピー
    p2.age = 25;

    // p1.age は 20 のまま
```
このように、値が直接メモリに保持されるので「独立したデータ」として扱われる。

<br><br><br>

## ✅ クラス（class）は 参照型

参照型 とは：

- 変数に入れるのは「実体への参照（アドレス）」。
- 代入すると「同じものを指す参照」が増えるだけ。
- だから片方を変えると、もう片方も変わる。

<br>

例（JavaScriptの class）：
```js
    class User {
      constructor(name) {
        this.name = name;
      }
    }

    const u1 = new User("Alice");
    const u2 = u1; // 参照をコピーしているだけ
    u2.name = "Bob";

    console.log(u1.name); // "Bob" になる！
```
`u1` と `u2` は 同じ実体（オブジェクト） を見ている。

<br><br><br><br><br>

# 🔍「オブジェクト」と「クラス」の区別
## 1️⃣ クラスとは？

クラスは「設計図」
「こういうデータを持っていて、こういう動きをするよ！」という 型 の定義。

例えば `User` クラスなら、

- nickname、old、birth、state というデータ（プロパティ）

- toString() という振る舞い（メソッド）

をまとめて「こういう構造を持つよ」と決めたもの。

<br>

```js
    class User {
      constructor(nickname, old, birth, state) {
        this.nickname = nickname;
        this.old = old;
        this.birth = birth;
        this.state = state;
      }

      format {
        return `User{ nickname: ${this.nickname} }`;
      }
    }
```
→ これはまだ「設計図」にすぎない。

<br><br><br>

## 2️⃣ オブジェクトとは？

オブジェクトは「実体（製品）」
クラス（設計図）を使って「`new`」で作られたモノがオブジェクト。

<br>

例えば：
```js
const user1 = new User("mako", 13, "08/08", "nara");
const user2 = new User("megumi", 14, "11/02", "saitama");
```
→ `user1` と `user2` は `User` クラス という型をもつ オブジェクト。

<br>

- `user1.nickname` は “`mako`”
- `user2.nickname` は “`megumi`”

同じ設計図から作っても、中身は違う！
→ だから「実体」と言う。

<br><br><br><br><br>

# 💡まとめ
## ✅ 【1】構造体（struct）とは？

- 複数のデータをひとまとめにする型（データの集まり）
- 例: `struct Person { name, age, height }`
- C言語などに多い
- メソッド（動作）を持たない → データだけ
- 値型 → 代入するとコピーが作られる
    → コピー後はお互い独立して動く

<br><br>

## ✅ 【2】クラス（class）とは？

- データ＋動作 をひとまとめにできる型
  - データ = プロパティ
  - 動作 = メソッド
- 例: `class User { constructor(...) {...} format() {...} }`
- `constructor` は 初期化専用の関数 → `new` で呼ばれる
- `this` は 作られたオブジェクト自身 を指す
- 参照型 → 代入すると「実体のアドレス」を共有する
    → コピーではなく同じものを見る

<br><br>

## ✅ 【3】オブジェクトとは？

- クラス（設計図）から作った「実体」
- 例:
```js
const user1 = new User("mako", 13, "08/08", "nara");
```
→ `user1` は `User` クラス型のオブジェクト
- `user1.nickname` で中のデータにアクセス
- 同じクラスでも、値はバラバラにできる

<br><br>

## ✅ 【4】構造体とクラスの比較
| 項目       | 構造体 (struct)         | クラス (class)                 |
|------------|-------------------------|--------------------------------|
| 型の性質   | 値型                    | 参照型                         |
| 定義       | `struct`                | `class`                        |
| メソッド   | 持たない（C言語の場合） | 持てる                         |
| コピー時   | 新しい実体が作られる    | アドレス（参照）を共有する     |
| 用途       | 軽量で独立したデータ    | 大きな機能をまとめたい時に便利 |

<br><br>

## ✅ 【5】クラスとオブジェクトの関係

- クラス = 設計図
  - どんなデータや機能を持つかを決める
- オブジェクト = 実体
    - クラスを `new` で作って初めてできる
- 例: 家の設計図（クラス） → 建てた家（オブジェクト）

<br><br>

## ✅ 【6】JavaScript でのポイント

- `class` は ES6 以降の機能
- `constructor` は 1 クラスに 1 つ
- `this.プロパティ` でオブジェクトに値をセットする
- `toString()` は文字列として表示する方法を定義できる

<br><br>

## ✅ 【7】構造体 ≒ クラス？

- どちらも「複数のデータをまとめる」点は同じ
- クラスはそれに「動作を加えられる拡張版」
- だから 構造体の延長 と思えばOK！

<br><br>

## ✨ まとめ一言

- `struct`: データをまとめるだけ
- `class`: データ＋動作をまとめる
- オブジェクト: クラスから作る具体的なモノ



<br><br><br>[僕の失敗談(´;ω;｀)と解決法🐈](https://paizabeginner.wordpress.com/about/)
