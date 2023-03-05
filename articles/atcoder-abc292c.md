---
title: "ABC292-C: Four Variables 解説"
emoji: "🟫"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [AtCoder]
published: true
---

## 問題(問題読解するとこんなことを言ってます)
> 正整数$N$が与えられるので，$AB + CD = N$を満たす$(A,B,C,D)$の組の個数を出力してください

### 制約
> $2 \leq N \leq 2 \times 10^5$
> 答えは$9 \times 10^{18}$以下であることが保証される

https://atcoder.jp/contests/abc292/tasks/abc292_c

## コンテスト中に考えたこと
- 計算量的に$O(N^2)$が通らない
- $AB=N$を満たす$(A,B)$の組の総数は$O(\sqrt(N))$で求められるのでこれを使えば良さそう
- $AB$か$CD$かのどちらかが決まれば両方決まるので，片方を$1$以上$N$以下で探索すると良さそう

## 解説
- $AB$を固定すると，$CD = N - AB$となる
- 積が$N$となるペアの総数を求める関数を$f(N)$とすると，答えは$\sum_{i=1}^{N-1}{f(i) \times f(N - i)}$
- 関数$f(N)$は積が$N$になるペアのうち，少なくとも一方は$\sqrt N$以下であることを用いることで$O(\sqrt N)$で動作する
- そのため全体として$O(N\sqrt N)$で解くことができる

::::details コード
```cpp
#include<bits/stdc++.h>
using ll = long long;
using namespace std;

ll countProductPairs(ll N){
  ll res = 0;
  for(ll i = 1; i * i <= N; ++i){
    if(N % i == 0){
      if(i * i == N) res += 1;
      else res += 2; // (A,B) = (i, N/i), (N/i, i)
    }
  }
  return res;
}

int main(){
  int N;
  cin >> N;

  ll ans = 0;
  for(ll i = 1; i < N; ++i){
    ans += countProductPairs(i) * countProductPairs(N - i);
  }
  cout << ans << endl;
}

```
::::
https://atcoder.jp/contests/abc292/submissions/39462617
