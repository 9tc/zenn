---
title: "ABC292-E: Transitivity 解説"
emoji: "💧"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [AtCoder]
published: true
---

## 問題
> $N$頂点$M$辺の有向グラフが与えられます
> 3頂点$a,b,c$について，辺$ab$と辺$bc$が存在するならば辺$ac$が存在するという条件を満たす状態になるまで，辺を追加します．
> 追加する必要のある辺の本数の最小値を出力してください

### 制約
> $3 \leq N \leq 2000$
> $0 \leq M \leq 2000$

https://atcoder.jp/contests/abc292/tasks/abc292_e

## コンテスト中に考えたこと
- 絵を書くと，ある頂点から辺を辿って到達可能な頂点には辺を直接追加する必要があって，それが最小っぽい

## 解説(解説になってなさそうです)
- グラフを受け取って，各頂点から到達可能な頂点のリストを求めることを考える
  - BFSだったりDFSだったり，計算量的に余裕あるのでdijkstraとかを使えばできる
- あとは直接1辺で到達可能な頂点の組を除いてカウントすればよい

::::details コード
```cpp
#include<bits/stdc++.h>
using namespace std;
#define INF (int)1e9

using Graph = vector<vector<int>>;


vector<int> dijkstra(int N, Graph& G, int s){
  vector<int> dist(N, INF);
  dist[s] = 0;
  priority_queue<pair<int,int>, vector<pair<int,int>>, greater<pair<int,int>>> pq;
  pq.emplace(0, s);
  while(!pq.empty()) {
    auto [nowCost, now] = pq.top(); pq.pop();
    if(dist[now] < nowCost) continue;
    for(auto to: G[now]){
      if(dist[to] > nowCost + 1){
        dist[to] = nowCost + 1;
        pq.emplace(nowCost + 1, to);
      }
    }
  }
  return dist;
}

int main(){
  int N, M;
  cin >> N >> M;
  Graph G(N);
  for(int i = 0; i < M; ++i){
    int u, v;
    cin >> u >> v;
    --u, --v;
    G[u].push_back(v);
  }

  vector<vector<int>> dist(N);
  for(int i = 0; i < N; ++i){
    dist[i] = dijkstra(N, G, i);
  }

  int ans = 0;
  for(int i = 0; i < N; ++i){
    for(int j = 0; j < N; ++j){
      if(i == j) continue;
      if(dist[i][j] != INF && dist[i][j] != 1) ++ans;
    }
  }
  cout << ans << endl;
}

::::

https://atcoder.jp/contests/abc292/submissions/39465592
