# 構造体の検索　（続 クラス・インスタンス）
  
  
前回に引き続きpaizaの構造体の問題に挑戦！

早く使いこなせるように練習あるのみ！

<br>

# 問題概要

- クラスの人数Nと、N人分の「名前・年齢・誕生日・出身地」の情報が渡される

- 最後に欲しい年齢Kが渡される

- K歳の生徒の名前を出力する
<br>

入力例：
    
    3
    mako 13 08/08 nara
    megumi 14 11/02 saitama
    taisei 16 12/04 nagano
    14

出力例：
    
    megumi

<br>

https://paiza.jp/works/mondai/class_primer/class_primer__find

<br><br><br><br><br>

# ✅ OKコード例：
```js
const rl = require('readline').createInterface({ input: process.stdin });

const lines = [];

rl.on('line', (input) => {
  lines.push(input);
});


rl.on('close', () => {
  // 1行目：クラスの人数 N を取得
  const N = Number(lines[0]);

  // N+1 行目：探したい年齢 K を取得
  const K = Number(lines[N + 1]);

  // ✅ クラスを定義
  class Student {
    // constructor は「new Student(...)」されたときに呼ばれる    
    constructor(name, old, birth, state) {
      // this は そのインスタンス自身 を指す
      this.name = name;     // 名前
      this.old = old;       // 年齢
      this.birth = birth;   // 誕生日
      this.state = state;   // 出身地
    }
  }



  // Student インスタンスを入れる配列
  const students = [];

  // 2行目〜N行目のデータを 1人ずつ処理
  for (let i = 1; i <= N; i++) {
    const [name, old, birth, state] = lines[i].split(' ');
    // ✅ new Student()で Student クラスから「インスタンス（実体）」を作る
    students.push(new Student(name, Number(old), birth, state));
  }

  // 年齢が K の生徒を探す
  for (const student of students) {
    if (student.old === K) {
      console.log(student.name);
      break; // 見つけたら終了
    }
  }
});
```
<br>

## 🔹 1. class Student は「設計図」

名前・年齢・誕生日・出身地を持つ、という型を定義している。

<br><br>

## 🔹 2. new Student(...) は「インスタンス化」

`new` を使うと、クラスの設計図から 1 つの実体（オブジェクト）を作る。

この実体を「インスタンス」と呼ぶ。

<br>

例：
```js
const s = new Student(...)
```
→ `s` は `Student` クラスのインスタンス。

👉 `new` を使った瞬間に、`constructor` が呼ばれて初期化が行われる。

<br><br>

## 🔹 3. this は「自分自身のデータ」

`constructor` の中で `this.name = name` のように書くことで、作られたそのインスタンスの中に値が保存される。

<br>

つまり、`new` → `constructor` → `this` という流れで
設計図（クラス）に値を入れて 1 つのモノ（インスタンス）を完成させる。

<br>

作った後は `student.old` のように `.` を使って、
そのインスタンスの中身を自由に取り出したり使える。

<br><br><br><br>

# 🗒️メモ

- `new` が設計図(`class`)を実物にするスイッチ。
- `constructor` が設計図にデータを流し込む工場。
- `this` はそのインスタンス自身を指し、工場の中でデータを詰め込む箱のような役割。


<br><br><br>[僕の失敗談(´;ω;｀)と解決法🐈](https://paizabeginner.wordpress.com/about/)


<br><br><br><br><br>

# ✅ OKコード例：コメントなし
```js
const rl = require('readline').createInterface({input:process.stdin});

const lines = [];

rl.on('line', (input) => {
    lines.push(input);
});


rl.on('close', () => {
    const N = Number(lines[0])
    const K = Number(lines[N+1]);
    
    class Student{
        constructor(name, old, birth, state){
            this.name = name;
            this.old = old;
            this.birth = birth;
            this.state = state;
        }
    }
    
    const students = [];
    for(let i = 1; i <= N; i++){
        const [name, old, birth, state] = lines[i].split(' ');
        students.push(new Student(name, Number(old), birth, state));
    }
    
    for(const student of students){
        if(student.old === K){
            console.log(student.name);
            break;
        }
    }
});
```
  

