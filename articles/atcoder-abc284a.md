---
title: "ABC284-A: Sequence of Strings 解説"
emoji: "🅰️"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [AtCoder]
published: true
---

## 問題
> $N$個の文字列$S_1,S_2,...,S_N$が与えられるので，$S_N,S_{N-1},...,S_1$の順で出力してください

https://atcoder.jp/contests/abc284/tasks/abc284_a

## 解説
- 配列とループを使うことができれば解ける
- サイズが$N$の文字列型(C++だとString型)の配列を用意し，for文を用いて入力，for文を用いて逆順で出力すれば良い

## コード

https://atcoder.jp/contests/abc284/submissions/37863292
