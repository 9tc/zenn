---
title: "ABC015-D: 高橋くんの苦悩 解説"
emoji: "💧"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [AtCoder]
published: true
---

## 問題(概要)
> 正整数$W$, $K$と$N$個の正整数の組$(A_1, B_1), (A_2, B_2) ,...,(A_N, B_N)$が与えられます．
> この$N$個の組から$K$個まで選びます．
> この時，選んだ組の$A$の総和は$W$以下である必要があります．
> この条件下の$B$の総和の最大値を出力してください．

### 制約
> $1 \leq W \leq 10000$
> $1 \leq K \leq N \leq 50$
> $1 \leq A_i \leq 1000$
> $1 \leq B_i \leq 100$

https://atcoder.jp/contests/abc015/tasks/abc015_4

## 解説
- ナップサック問題に選べる数の制約がついた感じの問題
- この制約だと次のような動的計画法で解ける
  - $dp[i][j][w] : (A_i, B_i)$の組までで$j$組選んだとき，$A$の総和が$w$の時の$B$の総和の最大値
  - $dp[i][j][w] \leftarrow max(dp[i][j][w], dp[i-1][j][w], dp[i-1][j-1][w - A_i] + B_i)$
- 計算量は$O(NKW)$, 制約の最大値であっても実行時間制限の2秒以内に十分間に合いそう

## コード

https://atcoder.jp/contests/abc015/submissions/37901372

## Tips
- 実行時間がC++でも124msとなっている
- この解答ではdpテーブルが3次元で表現されている．
- 実は$j$の操作を小さい順ではなく大きい順で行うことで，dpテーブルにおける$i$の情報は不要になるため，2次元で表現ができる(14行目の部分)．
  - 大きい順にしないで2次元で表現すると同じ組を2度選んでしまう可能性がある
  - たまに役立つので覚えておくとヨシ
  - これだと61ms

https://atcoder.jp/contests/abc015/submissions/37901875
