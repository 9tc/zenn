---
title: "ABC285-D: Change Usernames è§£èª¬"
emoji: "ð«"
type: "tech" # tech: æè¡è¨äº / idea: ã¢ã¤ãã¢
topics: [AtCoder]
published: true
---

## åé¡
> $N$äººãã¦$i$çªç®ã®äººã®ååã¯$S_i$ã§ãã
> $i$çªç®ã®äººã¯ååã$T_i$ã«å¤æ´ãããã§ãã
> é©åãªé åºã§ååãå¤æ´ãããã¨ã§2äººä»¥ä¸ã®äººãåãååã¨ãªãç¬éãå­å¨ããªãããã«å¨å¡ååãå¤æ´ãããã¨ãã§ãããå¤å®ãã¦ãã ããã

https://atcoder.jp/contests/abc285/tasks/abc285_d

## è§£èª¬
- $A$ããã$B$ã¨ããååã«ãããã$B$ããã$C$ã¨ããååã«ãããã¨ããæå ±ããã£ãæã$A$ããã¯$B$ãããååãå¤æ´ãã¦ããåºãªãã¨å¤æ´ã§ããªã
- ãã®æå ±ããååãã©ãã«ã¨ããæåã°ã©ãã§è¡¨ç¾ã§ãã
  - ä¸è¿°ã®ç¶æ³ã¯$A \rightarrow B \rightarrow C$ã¨ãªã
- ã°ã©ãã§è¡¨ç¾ããã¨ãã«æåéè·¯ãã§ããã¨ãããã®ãµã¤ã¯ã«ã«å«ã¾ããäººãã¡ã¯èª°ãååãå¤æ´ãããã¨ãã§ããªã
- ãµã¤ã¯ã«ãå­å¨ããããå¤å®ããã°è¯ã(ãµã¤ã¯ã«æ¤åºã¯ã°ã°ãã°åºãã®ã§ãããåã«å¤æ´ãã)
  - ä»åã®å¶ç´ä¸UnionFindã§å¤å®ãã¦ãOKããã
- æå­åã®åºç¾é ã§ã©ãã«ãæ¯ã£ã¦ãä¸è¬çãªã°ã©ãã¨ãã¦æ±ããã¯ããã¯ããã

https://qiita.com/drken/items/a803d4fc4a727e02f7ba#4-6-ãµã¤ã¯ã«æ¤åº

::::details ã³ã¼ã
```cpp
#include<bits/stdc++.h>
using namespace std;

using Graph = vector<vector<int>>;
vector<int> detectCycle(int n, Graph &g){
  const int UNUSED = 0;
  const int USING = 1;
  const int USED = 2;
  vector<int> status(n, UNUSED);
  vector<int> pre(n);
  vector<int> cycle;

  function<bool(int)> dfs = [&](int u) -> bool{
    status[u] = USING;
    for(auto &v: g[u]){
      if(status[v] == UNUSED){
        pre[v] = u;
        if(dfs(v)) return true;
      }else if(status[v] == USING){
        int cur = u;
        while(cur != v){
          cycle.push_back(pre[cur]);
          cur = pre[cur];
        }
        cycle.push_back(u);
        return true;
      }
    }
    status[u] = USED;
    return false;
  };

  for(int i = 0; i < g.size(); ++i){
    if(status[i] == UNUSED && dfs(i)){
      reverse(cycle.begin(), cycle.end());
      return cycle;
    }
  }
  return {};
};


int main(){
  int N;
  cin >> N;
  unordered_map<string, int> nameToI;
  vector<pair<int,int>> edge;
  for(int i = 0; i < N; ++i){
    string s, t;
    cin >> s >> t;
    int S, T;
    if(nameToI.count(s)) S = nameToI[s];
    else S = nameToI[s] = nameToI.size();

    if(nameToI.count(t)) T = nameToI[t];
    else T = nameToI[t] = nameToI.size();

    edge.push_back({S, T});
  }

  Graph G(nameToI.size());
  for(auto &[u, v]: edge) G[u].push_back(v);

  auto r = detectCycle(nameToI.size(), G);
  if(r.empty()) cout << "Yes" << endl;
  else cout << "No" << endl;
}
```
::::
https://atcoder.jp/contests/abc285/submissions/38103771
