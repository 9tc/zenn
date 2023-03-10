---
title: "ABC292-E: Transitivity è§£èª¬"
emoji: "ð§"
type: "tech" # tech: æè¡è¨äº / idea: ã¢ã¤ãã¢
topics: [AtCoder]
published: true
---

## åé¡
> $N$é ç¹$M$è¾ºã®æåã°ã©ããä¸ãããã¾ã
> 3é ç¹$a,b,c$ã«ã¤ãã¦ï¼è¾º$ab$ã¨è¾º$bc$ãå­å¨ãããªãã°è¾º$ac$ãå­å¨ããã¨ããæ¡ä»¶ãæºããç¶æã«ãªãã¾ã§ï¼è¾ºãè¿½å ãã¾ãï¼
> è¿½å ããå¿è¦ã®ããè¾ºã®æ¬æ°ã®æå°å¤ãåºåãã¦ãã ãã

### å¶ç´
> $3 \leq N \leq 2000$
> $0 \leq M \leq 2000$

https://atcoder.jp/contests/abc292/tasks/abc292_e

## ã³ã³ãã¹ãä¸­ã«èãããã¨
- çµµãæ¸ãã¨ï¼ããé ç¹ããè¾ºãè¾¿ã£ã¦å°éå¯è½ãªé ç¹ã«ã¯è¾ºãç´æ¥è¿½å ããå¿è¦ããã£ã¦ï¼ãããæå°ã£ã½ã

## è§£èª¬(è§£èª¬ã«ãªã£ã¦ãªãããã§ã)
- ã°ã©ããåãåã£ã¦ï¼åé ç¹ããå°éå¯è½ãªé ç¹ã®ãªã¹ããæ±ãããã¨ãèãã
  - BFSã ã£ããDFSã ã£ããï¼è¨ç®éçã«ä½è£ããã®ã§dijkstraã¨ããä½¿ãã°ã§ãã
- ãã¨ã¯ç´æ¥1è¾ºã§å°éå¯è½ãªé ç¹ã®çµãé¤ãã¦ã«ã¦ã³ãããã°ãã

::::details ã³ã¼ã
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
