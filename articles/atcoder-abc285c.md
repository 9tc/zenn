---
title: "ABC285-C: abc285_brutmhyhiizp 解説(二分探索解)"
emoji: "🔲"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [AtCoder]
published: true
---

## 問題
> 文字列がA,B,C,...,Y,Z,AA,AB,AC,...,ZY,ZZ,AAA,AAB,...と$10^{16}$個並んでいます。
> 文字列$S$が与えられるので、$S$は何番目か答えてください。

https://atcoder.jp/contests/abc285/tasks/abc285_c

## 解説
- ABC171-Cを知っていますか？私は知っています。
  - https://atcoder.jp/contests/abc171/tasks/abc171_c
  - やることはこの問題の逆で、$N$から文字列を作るだけ
  - 26進数と見立ててアルファベットを割り当てればOK
- この問題を解く関数を作ることができれば二分探索ができる
  - C++だと長さが一致すれば文字列を直接比較できるので楽です

::::details コード
```cpp
#include<bits/stdc++.h>
using ll = long long;
using namespace std;

string getABC171C(ll n){
  --n;
  string res;
  while(n >= 0){
    res += (n % 26 + 'A');
    n /= 26;
    --n;
  }
  reverse(res.begin(), res.end());
  return res;
}

int main(){
  string S;
  cin >> S;

  ll left = 1, right = 10000000000000001;
  while(right - left > 1){
    ll mid = (left + right) / 2;
    string T = getABC171C(mid);
    if(S.length() < T.length()) right = mid;
    else if(S.length() > T.length()) left = mid;
    else if(S < T) right = mid;
    else left = mid;
  }
  cout << left << endl;
}
```
::::
https://atcoder.jp/contests/abc285/submissions/38101138
