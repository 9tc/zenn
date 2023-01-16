---
title: "ABC285-A: Edge Checker 2 解説"
emoji: "🔲"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [AtCoder]
published: true
---

## 問題
> (実際の問題文は画像で示されています)
> 15頂点の完全二分木があります。$2 \leq i \leq 15$について頂点$i$と頂点$\left\lfloor \frac{i}{2} \right\rfloor$($\frac{i}{2}$の小数点以下切り捨て)は辺で結ばれています。
> 2つの整数$a$,$b$が与えられるので頂点$a$と頂点$b$が辺で結ばれているか判定してください。

https://atcoder.jp/contests/abc285/tasks/abc285_a

## 解説
- 全ての辺の情報を埋め込んでも解けるが、関係性を見つければすぐに解ける
- 制約として$a<b$があるので，$a$と$\frac{b}{2}$の切り捨てが一致するか判定すれば良い

## コード
```cpp
#include<bits/stdc++.h>
using namespace std;

int main(){
  int a, b;
  cin >> a >> b;

  if(a == b/2) cout << "Yes" << endl;
  else cout << "No" << endl;
}
```
https://atcoder.jp/contests/abc285/submissions/38099896
