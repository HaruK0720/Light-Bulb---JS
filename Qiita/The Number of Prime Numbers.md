# 素数の個数




今回はPaizaの「素数の個数を数える」問題に挑戦！

久しぶりだから忘れてたけど、「フラグ」を使うのがポイントだった！


<br>

## 問題概要

整数 N が与えられるので、2 以上 N 以下の素数の個数を求めよ。

<br>

入力例：

    100

出力例：

    25

<br>

https://paiza.jp/works/mondai/double_roop_problems/double_roop_problems__prime_number_easy

<br><br><br>

## ✅ OK例①：引き算スタイル
```js
let primeCount = N - 1;
for (let i = 3; i <= N; i++) {
  for (let j = 2; j < i; j++) {
    if (i % j === 0) {
      primeCount--;
      break;
    }
  }
}

console.log(primeCount);
```

### 💡ポイント：引き算スタイルの考え方

- 最初に `primeCount = N - 1` として、2 〜 N までの全てを「仮の素数」としてカウント（1は素数ではないので除外）。
    
- 外側のループ `i` は 3 からスタート。( 2 は最初から素数として数えられている)
    
- 内側のループ `j` は、2 から `i - 1` まで回す。1 と i 自身は必ず割り切れるので除外している。
    
- `i % j === 0` で割り切れたら、その時点で `i` は素数じゃない → `primeCount` を 1 減らしてループ終了（`break`）。


<br><br>

## ✅ OK例②：フラグ スタイル
```js
let primeCount = 0;
for (let i = 2; i <= N; i++) {
  let isPrime = true;
  for (let j = 2; j * j <= i; j++) {
    if (i % j === 0) {
      isPrime = false;
      break;
    }
  }
  if (isPrime) primeCount++;
}

console.log(primeCount);
```

### 💡ポイント：フラグ スタイルの考え方
- `isPrime = true` で始めて、1 個でも割り切れたら `false` にする。
    
- 内側のループの条件は `j * j <= i`。割る数は `i` の平方根まででOK！（これで大幅にループ数が減る）
    
- 割り切れた瞬間に `isPrime = false` として `break` → 無駄なループを避けて高速化。
    
- ループ後に `isPrime === true` のときだけ、`primeCount++` でカウントする。


<br><br><br>

## ✍️気づきメモ & まとめ

- 割り切れる＝素数じゃない という考え方。
    
- 素数かどうかのチェックは全部の数じゃなくて、√ i まででOKだった！（約数の考え方の応用）
    
- フラグ管理（`isPrime = true/false`）は思ってる以上に読みやすい
    
- `for` ループ内に `break` を使うと、無駄なループを防げて時短になる

- 数学の基本知識（素数の定義）が、コードの理解にも役立つ




<br><br><br>[僕の失敗談(´;ω;｀)と解決法🐈](https://paizabeginner.wordpress.com/2025/06/18/paiza%e3%81%a7%e5%9f%ba%e6%9c%ac%e3%83%9e%e3%82%b9%e3%82%bf%e3%83%bc%ef%bc%9a%e7%b4%a0%e6%95%b0%e3%81%ae%e5%80%8b%e6%95%b0/)
