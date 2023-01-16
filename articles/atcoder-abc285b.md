---
title: "ABC285-B: Longest Uncommon Prefix 解説"
emoji: "🔲"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [AtCoder]
published: true
---

## 問題
> 長さ$N$の文字列$S$が与えられます。
> $i = 1, 2, ..., N-1$のそれぞれについて、次の条件を満たす最大の非負整数$l$を求めてください。
>> $l + i \leq N$
>> 全ての$1 \leq k \leq l$を満たす整数$k$について、$S$の$k$文字目と$S$の$k+i$文字目は異なる。

https://atcoder.jp/contests/abc285/tasks/abc285_b

## 解説
- ぱっと見問題がわかりにくいが，頑張って読解してコードを書こう(投げやり)
- こういうときは入出力例を見るとイメージしやすい

::::details コード
```cpp
#include<bits/stdc++.h>
using namespace std;

int main(){
  int N;
  cin >> N;
  string S;
  cin >> S;

  for(int i = 1; i <= N-1; ++i){
    int ans = 0;
    for(int l = 0; l < N; ++l){
      if(l + i >= N) break;
      if(S[l] == S[l+i]) break;
      ++ans;
    }
    cout << ans << endl;
  }
}
```
::::
https://atcoder.jp/contests/abc285/submissions/38100649
