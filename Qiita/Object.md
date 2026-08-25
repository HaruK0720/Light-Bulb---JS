# 背の順　　おまけ：オブジェクト

今日はpaizaの渡されたリストを元に「背の順」に並び替える問題に挑戦！

久しぶりに `Map()` を使ったけど、結局不要だったみたい😆

あと、おまけでオブジェクトについて勉強してみた！

<br>

# 問題概要

- 生徒数 N と、各生徒の「身長」と「名前」が渡される

- 身長が高い順に並べ替えて、名前だけを上から出力する

<br>

入力例:

    3
    173 Hashimoto
    195 Yamamoto
    113 Yoshida

出力例:

    Yamamoto
    Hashimoto
    Yoshida

<br>

https://paiza.jp/works/mondai/rank_test_problems_c_0001/rank_test_problems_c_0001__4

<br><br><br><br>

# 🔺OK？NG？例：
```js
const rl = require('readline').createInterface({ input:process.stdin });
const lines = [];

rl.on('line', (input) => {
    lines.push(input);
});


rl.on('close', () => {
    const N = Number(lines[0]);
    const arrA =lines.splice(1).map(line => line.split(' ')); 
    
    const height = new Map();
    for(let i = 0; i < N; i++){
        height.set(arrA[i][0], arrA[i][1]);
    }
    
    const order = [...height.keys()].sort((a,b) => b-a);
    
    order.forEach(h => {
        console.log(height.get(h));
    })
    
});
```
一応、paizaのテストケースは全て ✅正解判定 だったけども、

同じ身長の人がいると 後から登録した人に上書きされてしまう！

<br><br><br><br>

# ✅OK例：
```js
const rl = require('readline').createInterface({ input:process.stdin });
const lines = [];

rl.on('line', (input) => {
    lines.push(input);
});


rl.on('close', () => {
    const N = Number(lines[0]);
    const arrA =lines.splice(1).map(line => line.split(' ')); 
    
    const order = arrA.sort((a,b) => b[0] - a[0]);
    
    order.forEach(a => {
        console.log(a[1]);
    })
    
});
```
配列に[身長, 名前]をセットでして、ソート条件で先頭の要素（身長）を降順にすればOK！（`b[0] – a[0]`）

<br><br><br><br>

# 🗒️メモ

- `Map` は同じキー（同じ身長）で上書きされるのでNG！

- 文字列のままソートすると数値順じゃなく辞書順になる罠あり

- `sort()` で数値ソートする場合は必ず `b - a`！(背の高い順)

<br><br><br>[僕の失敗談(´;ω;｀)と解決法🐈](https://paizabeginner.wordpress.com/about/)

<br><br><br><br>

# 💡おまけ：オブジェクト

やってることは二次元配列のやり方と同じだけど、`Map`と同じで（身長）キーが重複したらアウト❌

でも、触れたことなかったから、そろそろオブジェクトを勉強して試してみる！

<br><br>

## ✅ オブジェクトの基本構造
```js
const student = {
  height: 173,
  name: "Hashimoto"
};
```
ここで `student` はオブジェクトで、
`height` と `name` という キー（プロパティ名） と
それぞれの 値（バリュー） を持っている。

<br><br><br>

## ✅ 値を取り出す方法

オブジェクトから値を取り出す方法は主に2つ
<br>

### 1️⃣ ドット記法 .

書き方：
```js
student.height  // 173
student.name    // "Hashimoto"
```
- オブジェクト.プロパティ名

<br>

### 2️⃣ ブラケット記法 []

書き方：
```js
student["height"]  // 173
student["name"]    // "Hashimoto"
```
- オブジェクト["プロパティ名"]

- 文字列としてキーを指定する。

<br><br><br>

### ✅ いつ [] を使う？

- キー名を変数で動的に指定したいとき
```js
const key = "height";
console.log(student[key]);  // 173
```
<br>

- キー名に空白や特殊文字が含まれていて、ドットで書けないとき
```js
const obj = { "my height": 173 };
console.log(obj["my height"]);  // OK
// obj.my height ←これはエラー
```

<br><br><br>

## ✅ なぜオブジェクトにまとめると便利か？

例えば：
```js
students.sort((a, b) => b.height - a.height);
```
- `a` は `{ height: 173, name: "Hashimoto" }`
- `b` も同じ形

なので `a.height` を参照すれば身長、`a.name` で名前がすぐ取れる。

<br>

配列だけで分けてたら：
```
[173, "Hashimoto"]
```
みたいな形だと、どっちがどっちかは インデックス（0番、1番）に依存 するので可読性が落ちる。

<br><br<br>

## 🔑 まとめ

- `.` で中身を引き出せる
- `[]` は文字列や変数でキーを動的に扱える
- オブジェクトにまとめると「セットで管理」できる
- 並び替えしても紐づけが壊れない
- キーは文字列限定（Symbol は例外だけど基本は文字列）
- 同じキーを後から追加すると上書きされる
        → 同じキーで複数の値を同時に保持するのは不可


<br><br><br><br>

## 💡今回の問題でのコード例
```js
const rl = require('readline').createInterface({ input: process.stdin });
const lines = [];

rl.on('line', (input) => {
  lines.push(input);
});

rl.on('close', () => {
  const N = Number(lines[0]);

  //オブジェクト
  const students = lines.slice(1).map(line => {
    const [height, name] = line.split(' ');
    return { height: Number(height), name };
  });


  students.sort((a, b) => b.height - a.height);

  students.forEach(student => console.log(student.name));
});
```

### ✅ 何をしているか？分解して解説
```js
const students = lines.slice(1).map(line => {
  const [height, name] = line.split(' ');
  return { height: Number(height), name };
});
```
これを分解すると：

1️⃣ `lines.slice(1)`
→ 1行目の「N」は要らないので、2行目以降を取得。

例：
```
["173 Hashimoto", "195 Yamamoto", "113 Yoshida"]
```
<br>

2️⃣ `.map(...)`
→ 各行 `"173 Hashimoto"` を `split(' ')` で
`[ "173", "Hashimoto" ]` にする。

<br>

3️⃣ `return { height: Number(height), name };`
→ 分割代入で `height` と `name` に分けて、
```
{ height: 173, name: "Hashimoto" }
```
のようなオブジェクトを返す。

<br><br>

結果として、`students` はこうなる：
```js
[
  { height: 173, name: "Hashimoto" },
  { height: 195, name: "Yamamoto" },
  { height: 113, name: "Yoshida" }
]
```

<br><br><br>

### ✅ なんでオブジェクトにするのか

「身長」と「名前」を一緒に扱いたい から。

- 身長だけだと名前を忘れる
- 名前だけだと身長がわからない
- `Map` にするほど複雑でもない

なので、1つの要素に両方を まとめる箱 として、
`{ height, name }` にする。

<br><br>

### ✅ どう使うのか
1.ソートで便利
```js
students.sort((a, b) => b.height - a.height);
```
- `a` と `b` はオブジェクト `{ height, name }` だから

- `b.height - a.height` として簡単に比較できる

<br>

2.出力で便利

```js
students.forEach(student => console.log(student.name));
```
  

- `student` は `{ height, name }`

- `student.name` で名前だけ取れる(`student`はソート済み)


<br><br><br>[僕の失敗談(´;ω;｀)と解決法🐈](https://paizabeginner.wordpress.com/about/)
