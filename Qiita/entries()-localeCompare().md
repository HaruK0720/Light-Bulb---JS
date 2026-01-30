# 文字列の出現回数をentries()とlocaleCompare()でスッキリ解決！

どうも、Paizaで修行中の男子高校生です！

今回はPaizaの問題集から「文字列の出現回数を辞書順でカウントして出力する」という、データ構造（`Map`）の理解を深めるにはもってこいの問題に挑戦したよ！

## <br>🧩 問題の内容

文字列がN個与えられます。
各文字列の出現回数を、文字列の辞書順に出力してください。

<br>📥 入力例
```
5
bcd
abc
bcd
bcd
bcd
```
📤 出力例
```
abc 1
bcd 4
```

<br>

https://paiza.jp/works/mondai/data_structure/data_structure__dict_step3


## <br>👊 最初に書いたバージョン
```js
const rl = require('readline').createInterface({input:process.stdin});
const lines = [];

rl.on('line',(input)=>{
    lines.push(input);
});

rl.on('close',()=>{
    const N = Number(lines[0]);
    const str = new Map();
    
    for(let i = 1; i <= N; i++){
        if(str.has(lines[i])){
            str.set(lines[i], str.get(lines[i]) + 1)
        }else{
            str.set(lines[i], 1);
        }
    }
    
    const keys = Array.from(str.keys()).sort();
    
    keys.forEach(a=>{
        console.log(a, str.get(a));
    });
});
```
正直、これでも正解出せたけど、`if`で分岐して`set`するのがちょっと面倒…

## <br>✅ スマートなバージョンはこちら！
```js
const rl = require('readline').createInterface({ input: process.stdin });
const lines = [];

rl.on('line', (input) => lines.push(input));

rl.on('close', () => {
    const countMap = new Map();

    lines.slice(1).forEach(word => {
        countMap.set(word, (countMap.get(word) || 0) + 1);
    });

    [...countMap.entries()]
        .sort((a, b) => a[0].localeCompare(b[0]))
        .forEach(([word, count]) => {
            console.log(word, count);
        });
});
```


# <br>🔍 解説いっぱい！

## <br>🧠 countMap.set(word, (countMap.get(word) || 0) + 1)
```js
countMap.get(word)
```
→ 今までにその単語が登録されてればカウント（例：`3`）

→ 登録されてなければ `undefined`
<br>
```js
countMap.get(word) || 0
```
→ 未登録なら `undefined || 0 → 0` になる！

つまり… 「まだ出てきてなければ 0 からカウント開始」ってこと！

## <br>🔧 [...countMap.entries()]

`entries()` は `Map` の中身（`key`, `value`のペア）を取り出すメソッド。

`MapIterator` っていう特殊な形式だから、[`...`]（スプレッド構文）で 普通の配列に変換！
```js
const map = new Map();
map.set("apple", 3);
map.set("banana", 2);

const iterator = map.entries(); 
console.log(iterator); 
// → MapIterator { ['apple', 3], ['banana', 2] }

// スプレッド構文を使って配列に変換
const array = [...iterator];
console.log(array); 
// → [ ['apple', 3], ['banana', 2] ]
```

## <br>🔡 .sort((a, b) => a[0].localeCompare(b[0]))

`a` と `b` は `[word, count]` の形の配列。

`a[0]` が単語だから、それを `localeCompare()` で比較！
```js
console.log("apple".localeCompare("banana")); // -1（辞書順で前）
console.log("banana".localeCompare("apple")); // 1（後）
console.log("apple".localeCompare("apple"));  // 0（同じ）
```
通常の `.sort()` だけだと、日本語や他の言語でうまく並ばないこともある。

`localeCompare()` を使えば、**人間が読む「自然な並び」**になる！

## <br>🔁 .forEach(([word, count]) => { ... })

分割代入で `[word, count]` を取り出して、`console.log`！
```js
.forEach(([word, count]) => {
    console.log(word, count);
});
```

## <br>🎯まとめ：この一連の流れ、1行ずつちゃんと意味ある！
```js
[...countMap.entries()] // Map → 配列
  .sort(...)            // 辞書順ソート
  .forEach(...)         // 出力
```


<br><br>[僕の失敗談(´;ω;｀)と解決話🚀](https://paizabeginner.wordpress.com/2025/04/17/paiza%e3%81%a7%e5%9f%ba%e6%9c%ac%e3%83%9e%e3%82%b9%e3%82%bf%e3%83%bc%ef%bc%9a%e6%96%87%e5%ad%97%e5%88%97%e3%81%ae%e5%87%ba%e7%8f%be%e5%9b%9e%e6%95%b0%e3%82%92entries%e3%81%a8localecompare%e3%81%a7/)

