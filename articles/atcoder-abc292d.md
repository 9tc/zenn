---
title: "ABC292-D: Unicyclic Components 解説"
emoji: "🟫"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [AtCoder]
published: true
---

## 問題
> $N$頂点$M$辺の無向グラフが与えられます
> 全ての連結成分について頂点数と辺数が一致するならYesを，そうでないならNoを出力してください

### 制約
> $1 \leq N \leq 2 \times 10^5$
> $0 \leq M \leq 2 \times 10^5$

https://atcoder.jp/contests/abc292/tasks/abc292_d

## コンテスト中に考えたこと
- UnionFindを使えば連結成分に分けることができる
- 一旦それぞれの頂点がどの連結成分に属するかをみて，その後辺の数を数えたらいいんでない

## 解説
- まずUnionFindを使って連結成分ごとに分ける

https://algo-method.com/tasks/431/editorial
- それぞれの頂点がどの連結成分に属するかを求める
  - UnionFindの根を求める関数を使えば良い
- 辺の情報からそれぞれの連結成分に何個の辺が存在するか数える

::::details コード
```cpp
#include<bits/stdc++.h>
#include <atcoder/all>
using namespace std;
using namespace atcoder;

int main(){
  int N, M;
  cin >> N >> M;
  vector<int> u(M), v(M);
  for(int i = 0; i < M; ++i){
    cin >> u[i] >> v[i];
    u[i]--, v[i]--;
  }

  dsu uf(N);
  for(int i = 0; i < M; ++i) uf.merge(u[i], v[i]);

  // それぞれの頂点がどの連結成分に属するかを求める
  vector<int> groupId(N);
  for(int i = 0; i < N; ++i) groupId[i] = uf.leader(i);

  // それぞれの連結成分に含まれる頂点数を数える
  vector<int> groupVertexNum(N, 0);
  for(int i = 0; i < N; ++i) groupVertexNum[groupId[i]]++;

  // それぞれの連結成分に含まれる辺数を数える
  vector<int> groupEdgeNum(N, 0);
  for(int i = 0; i < M; ++i) groupEdgeNum[groupId[u[i]]]++;

  // それぞれの連結成分で頂点数と辺数が一致しないものがあればNo
  for(int i = 0; i < N; ++i){
    if(groupVertexNum[i] != groupEdgeNum[i]){
      cout << "No" << endl;
      return 0;
    }
  }
  cout << "Yes" << endl;
}

```
::::
https://atcoder.jp/contests/abc292/submissions/39463735

## Tips
- union by sizeなUnionFindに辺の数を持たせるというやり方もあるみたいです

::::details 元にするUnionFind
```cpp
struct UnionFind {
  vector<int> parent;
  vector<int> size;

  UnionFind(int n) {
    parent.resize(n);
    size.resize(n);
    for(int i = 0; i < n; ++i){
      parent[i] = i;
      rank[i] = 0;
    }
  }

  int leader(int x) {
    if(parent[x] == x) return x;
    return parent[x] = leader(parent[x]);
  }

  bool merge(int x, int y) {
    x = leader(x);
    y = leader(y);
    if(x == y) return false;
    if(rank[x] < rank[y]) swap(x, y);
    if(rank[x] == rank[y]) ++rank[x];
    parent[y] = x;
    return true;
  }
};

```
::::

::::details このようにです
```diff cpp
struct UnionFind {
  vector<int> parent;
  vector<int> size;
+ vector<int> edgeCnt;

  UnionFind(int n){
    parent.resize(n);
    size.resize(n);
+   edgeCnt.resize(n);
    for(int i = 0; i < n; ++i){
      parent[i] = i;
      size[i] = 1;
+     edgeCnt[i] = 0;
    }
  }

  int leader(int x) {
    if(parent[x] == x) return x;
    return parent[x] = leader(parent[x]);
  }

  bool merge(int x, int y) {
    x = leader(x);
    y = leader(y);
    if(x == y){
+     edgeCnt[x]++;
      return false;
    }
    if(size[x] < size[y]) swap(x, y);
    parent[y] = x;
    size[x] += size[y];
+   edgeCnt[x] += edgeCnt[y] + 1;
    return true;
  }

+ bool equalsNumVerticesAndNumEdges(int x){
+   return size[leader(x)] == edgeCnt[leader(x)];
+ }
};
```
::::

::::details こうするとこう解けます main関数がシンプルです
```cpp
#include<bits/stdc++.h>
#include <atcoder/all>
using namespace std;
using namespace atcoder;

struct UnionFind {
  vector<int> parent;
  vector<int> size;
  vector<int> edgeCnt;

  UnionFind(int n){
    parent.resize(n);
    size.resize(n);
    edgeCnt.resize(n);
    for(int i = 0; i < n; ++i){
      parent[i] = i;
      size[i] = 1;
      edgeCnt[i] = 0;
    }
  }

  int leader(int x) {
    if(parent[x] == x) return x;
    return parent[x] = leader(parent[x]);
  }

  bool merge(int x, int y) {
    x = leader(x);
    y = leader(y);
    if(x == y){
      edgeCnt[x]++;
      return false;
    }
    if(size[x] < size[y]) swap(x, y);
    parent[y] = x;
    size[x] += size[y];
    edgeCnt[x] += edgeCnt[y] + 1;
    return true;
  }

  bool equalsNumVerticesAndNumEdges(int x){
    return size[leader(x)] == edgeCnt[leader(x)];
  }
};

int main(){
  int N, M;
  cin >> N >> M;
  UnionFind uf(N);
  for(int i = 0; i < M; ++i){
    int u, v;
    cin >> u >> v;
    uf.merge(u-1, v-1);
  }

  // それぞれの連結成分で頂点数と辺数が一致しないものがあればNo
  for(int i = 0; i < N; ++i){
    if(!uf.equalsNumVerticesAndNumEdges(i)){
      cout << "No" << endl;
      return 0;
    }
  }
  cout << "Yes" << endl;
}

```

https://atcoder.jp/contests/abc292/submissions/39464374
::::
