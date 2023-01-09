---
title: "ABC222-E: Red and Blue Tree 解説"
emoji: "💧"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [AtCoder]
published: true
---

## 問題
> $N$頂点の木グラフ, 数列$A_1, ..., A_M$, 整数$K$が与えられます
> それぞれの辺を赤か青かに塗ることを考える時，次の条件を満たす組合せの総数をmod 998244353で答えてください
>   駒を$A_1, A_2,..., A_M$と最短経路で動かした時に 赤の辺を通った回数 - 青の辺を通った回数 がKと等しい
>
https://atcoder.jp/contests/abc222/tasks/abc222_e

## 解説
- 次のステップに分解する
1. 頂点$A_1$から頂点$A_2$の最短経路，頂点$A_2$から頂点$A_3$の最短経路，...，頂点$A_{M-1}$から頂点$A_M$の最短経路を求める
   - dijkstra法 + 経路復元で十分間に合う
https://algo-logic.info/dijkstra/#toc_id_2
2. それぞれの最短経路の情報を元に，どの辺を何回通るかカウントする
3. $dp[i][j]$: $i$番目までの辺を塗った時に 赤の辺を通った回数 - 青の辺を通った回数が$j$となる組合せの総数
   - jが負の値をとるので$vector<map<int, modint>>$を使うと便利
4. $dp[n][k]$を出力

## コード
https://atcoder.jp/contests/abc222/submissions/37767369
