---
title: "ABC284-C: Count Connected Components 解説"
emoji: "🔲"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [AtCoder]
published: true
---

## 問題
> $N$頂点$M$辺の単純無向グラフが与えられます．
> 連結成分の個数を求めてください．
https://atcoder.jp/contests/abc284/tasks/abc284_c

## 解説
- UnionFindを使った典型的な問題です
  - DFSやBFSを使って連結している頂点を見つける方法でもできます
- UnionFind(Disjoint Set Union, dsu)は次の操作を高速に行うことができるデータ構造(?)です
  1. (Union) ある2つの要素を同じグループにする
  2. (Find) ある2つの要素が同じグループに存在するか判定する
  - 詳しくはググるとたくさんの先人の知恵があります．
- 今回の問題では，ある辺で繋がれた2つの頂点を同じグループにして，最終的にグループが何個あるか判定すれば良いです．
- AtCoderにはAtCoder Libraryというものが存在し，そのなかのdsuを用いると便利です．
  - groupsという関数が用意されていて，そのサイズを出力するだけになります

## コード

https://atcoder.jp/contests/abc284/submissions/37863681
