# 格子点



Paizaの「格子点」の最大積を求める問題に挑戦！

初めは動けばいいやと無駄な計算が多かったけど、問題文の条件を利用して、無駄を削減できた！

<br>

# 問題概要

- x + y < 100
- x³ + y³ < 100000

この2つの条件を満たす組み合わせの中で、x × y の最大値を求めよ。

※ x + y < 100 の制限で調べる候補は約4,300通り。全ての組を調べても実行時間制限に間に合う。

<br>

https://paiza.jp/works/mondai/double_roop_problems/double_roop_problems__grid_point

<br><br>

# △OK例：
```js
let max = -Infinity;

for (let x = 1; x <= 98; x++){
    
    for (let y = 1; y <= 98; y++){
        
        if (x ** 3 + y ** 3 < 100000){
            const temp = x * y;
            
            if (temp > max){
                max = temp;
            }
        }
    }
    
}
```
でも、内側のループに無駄な計算が見られる…

<br><br>

# ✅ OK例
```js
let max = -Infinity;

for (let x = 1; x <= 98; x++){
    
    for (let y = 1; x + y < 100; y++){
        
        if (x ** 3 + y ** 3 < 100000){
            const temp = x * y;
            
            if (temp > max) max = temp;
        }
    }
}


console.log(max);console.log(max);
```

内側ループの条件に `x + y < 100` を入れて、明らかに条件を満たさない `y` を調べる無駄をカット！

結果は変わらないのに処理はずっとスリム✨

<br><br>

# 🗒️ 気づきメモ & まとめ

- 二重ループは外側・内側のループ条件で検索範囲を工夫できる
- 問題の条件をループの範囲に反映するだけで効率アップ！
- 最初は動けばOK。でも次は「どうやって早く？」を考えてみる


<br><br><br>[僕の失敗談(´;ω;｀)と解決法🐈](https://paizabeginner.wordpress.com/2025/06/22/paiza%e3%81%a7%e5%9f%ba%e6%9c%ac%e3%83%9e%e3%82%b9%e3%82%bf%e3%83%bc%ef%bc%9a%e6%a0%bc%e5%ad%90%e7%82%b9/)
