---
title: "ABC284-E: Count Simple Paths 解説"
emoji: "🟩"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [AtCoder]
published: true
---

## 問題
> $N$頂点$M$辺の単純無向グラフが与えられます．各頂点の次数は$10$以下です．
> 頂点$1$を始点とする単純パスの個数を出力してください．ただし$10^6$を超える場合は代わりに$10^6$を出力してください．
https://atcoder.jp/contests/abc284/tasks/abc284_e

## 解説
- DFSを使って解く．Nが大きいので動的計画法で解きたくなる気持ちをグッと抑えよう．
- 実際に数え上げる数は$10^6$以上になった時点で打ち切って良いので，DFSで数え上げることができる．
  - 既に通った頂点とパスの端を管理するとうまく数え上げることができる．
  - 既に通った頂点は参照渡しをうまく活用することでコピーを防ぐ必要がある
    - コピーをするとDFSの1度の呼び出しが$O(N)$になるので$TLE$になる
      - https://atcoder.jp/contests/abc284/submissions/37865084

## コード

https://atcoder.jp/contests/abc284/submissions/37865029
