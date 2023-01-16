---
title: "ABC285-D: Change Usernames 解説"
emoji: "🟫"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [AtCoder]
published: true
---

## 問題
> $N$人いて$i$番目の人の名前は$S_i$です。
> $i$番目の人は名前を$T_i$に変更したいです。
> 適切な順序で名前を変更することで2人以上の人が同じ名前となる瞬間が存在しないように全員名前を変更することができるか判定してください。

https://atcoder.jp/contests/abc285/tasks/abc285_d

## 解説
- $A$さんが$B$という名前にしたい、$B$さんが$C$という名前にしたいという情報があった時、$A$さんは$B$さんが名前を変更してから出ないと変更できない
- この情報から名前をラベルとした有向グラフで表現できる
  - 上述の状況は$A \rightarrow B \rightarrow C$となる
- グラフで表現したときに有向閉路ができるとき、そのサイクルに含まれる人たちは誰も名前を変更することができない
- サイクルが存在するかを判定すれば良い(サイクル検出はググれば出るのでそれを元に変更する)
  - 今回の制約上UnionFindで判定してもOKらしい
- 文字列の出現順でラベルを振って、一般的なグラフとして扱うテクニックがある

https://qiita.com/drken/items/a803d4fc4a727e02f7ba#4-6-サイクル検出

::::details コード
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
