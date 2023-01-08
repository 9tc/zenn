---
title: "ABC284-D: Happy New Year 2023 解説"
emoji: "🎍"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [AtCoder]
published: true
---

## 問題
> $T$個のテストケースについて次の問題を解いてください
> 正整数$N$が与えられます．
> $N = p^2q(p, qは相異なる素数)$です．
> $p$と$q$を求めてください
https://atcoder.jp/contests/abc284/tasks/abc284_d

## 解説
- (前提) 32bit整数(int)だと扱いきれないので，64bit整数(long long)を使いましょう
- $N$の制約が$1 \leq N \leq 9 \times 10^{18}$なので工夫する必要がある
- $p$と$q$のうち，少なくとも片方が$3 \times 10^6$以下であることを使う
  - 両方が$3 \times 10^6$を超える場合，$N$は$(3 \times 10 ^ 6) ^ 3 = 27 \times 10^{18}$を超えるため，制約違反となる
- どちらか片方を決めるともう片方も決まるので，それを用いて判定する
  - 小さい方から順に判定するようにすると，そもそも素数か判定する必要がない(C++が高速だからかも?)
    - $N = p^2q$より，$N$を割り切れる数は$p, q, p^2, pq, p^2q$しか存在しないため，小さい方から判定すると$p$か$q$か小さい方が先に現れる

## コード

https://atcoder.jp/contests/abc284/submissions/37864047
