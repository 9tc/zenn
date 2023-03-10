---
title: "ABC292-D: Unicyclic Components è§£èª¬"
emoji: "ð«"
type: "tech" # tech: æè¡è¨äº / idea: ã¢ã¤ãã¢
topics: [AtCoder]
published: true
---

## åé¡
> $N$é ç¹$M$è¾ºã®ç¡åã°ã©ããä¸ãããã¾ã
> å¨ã¦ã®é£çµæåã«ã¤ãã¦é ç¹æ°ã¨è¾ºæ°ãä¸è´ãããªãYesãï¼ããã§ãªããªãNoãåºåãã¦ãã ãã

### å¶ç´
> $1 \leq N \leq 2 \times 10^5$
> $0 \leq M \leq 2 \times 10^5$

https://atcoder.jp/contests/abc292/tasks/abc292_d

## ã³ã³ãã¹ãä¸­ã«èãããã¨
- UnionFindãä½¿ãã°é£çµæåã«åãããã¨ãã§ãã
- ä¸æ¦ããããã®é ç¹ãã©ã®é£çµæåã«å±ããããã¿ã¦ï¼ãã®å¾è¾ºã®æ°ãæ°ããããããã§ãªã

## è§£èª¬
- ã¾ãUnionFindãä½¿ã£ã¦é£çµæåãã¨ã«åãã

https://algo-method.com/tasks/431/editorial
- ããããã®é ç¹ãã©ã®é£çµæåã«å±ããããæ±ãã
  - UnionFindã®æ ¹ãæ±ããé¢æ°ãä½¿ãã°è¯ã
- è¾ºã®æå ±ããããããã®é£çµæåã«ä½åã®è¾ºãå­å¨ãããæ°ãã

::::details ã³ã¼ã
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

  // ããããã®é ç¹ãã©ã®é£çµæåã«å±ããããæ±ãã
  vector<int> groupId(N);
  for(int i = 0; i < N; ++i) groupId[i] = uf.leader(i);

  // ããããã®é£çµæåã«å«ã¾ããé ç¹æ°ãæ°ãã
  vector<int> groupVertexNum(N, 0);
  for(int i = 0; i < N; ++i) groupVertexNum[groupId[i]]++;

  // ããããã®é£çµæåã«å«ã¾ããè¾ºæ°ãæ°ãã
  vector<int> groupEdgeNum(N, 0);
  for(int i = 0; i < M; ++i) groupEdgeNum[groupId[u[i]]]++;

  // ããããã®é£çµæåã§é ç¹æ°ã¨è¾ºæ°ãä¸è´ããªããã®ãããã°No
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
- union by sizeãªUnionFindã«è¾ºã®æ°ãæãããã¨ããããæ¹ãããã¿ããã§ã

::::details åã«ããUnionFind
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

::::details ãã®ããã«ã§ã
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

::::details ããããã¨ããè§£ãã¾ã mainé¢æ°ãã·ã³ãã«ã§ã
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

  // ããããã®é£çµæåã§é ç¹æ°ã¨è¾ºæ°ãä¸è´ããªããã®ãããã°No
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
