---
title: "ABC292-B: Yellow and Red Card 解説"
emoji: "🔲"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [AtCoder]
published: true
---

## 問題(問題読解するとこんなことを言ってます)
> $N$人いて，それぞれの人は0ポイント持ってます
> $Q$回$c$と$x$を受け取り対話します
>   $c$が1もしくは2ならば，人$x$のポイントを$c$ポイント増やします
>   $c$が3ならば，人$x$のポイントが$2$以上かどうか答えてください

### 制約
> $1 \leq N \leq 100$
> $1 \leq Q \leq 100$
> $1 \leq x \leq N$

https://atcoder.jp/contests/abc292/tasks/abc292_b

## 解説
- 愚直にやるだけ
- 問題文が長いが，やることはシンプル
  - 配列でポイントを管理してあげれば良い

::::details コード
```cpp
#include<bits/stdc++.h>
using namespace std;

int main(){
  int N, Q;
  cin >> N >> Q;

  vector<int> point(N, 0);
  while(Q--){
    int c, x;
    cin >> c >> x;
    if(c == 1 || c == 2) point[x-1] += c;
    if(c == 3){
      if(point[x-1] >= 2) cout << "Yes" << endl;
      else cout << "No" << endl;
    }
  }
}
```
::::
https://atcoder.jp/contests/abc292/submissions/39461742
