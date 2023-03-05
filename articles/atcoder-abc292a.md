---
title: "ABC292-A: CAPS LOCK 解説"
emoji: "🔲"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [AtCoder]
published: true
---

## 問題(概要)
> 英小文字からなる文字列$S$が与えられるので，全て大文字にして出力してください

### 制約
> $1 \leq |S| \leq 100$

https://atcoder.jp/contests/abc292/tasks/abc292_a

## 解説
- 大文字に変換する関数(C++だとtoupper関数)を使うと便利
- ASCIIコードを直接扱うことに慣れると良い
  - char型を数とみて足したり引いたりすると文字の変換ができる
    - 'A' + 1 -> 'B'みたいな
  - 今回は小文字を大文字に変換するので，各文字に'A' - 'a'を足してあげれば大文字になる

::::details コード
```cpp
#include<bits/stdc++.h>
using namespace std;

int main(){
  string S;
  cin >> S;
  for(char &c: S) c += 'A' - 'a';
  cout << S << endl;
}
```
::::
https://atcoder.jp/contests/abc292/submissions/39461501

::::details こういうのは関数に分けてあげたらみやすいです
```cpp
#include<bits/stdc++.h>
using namespace std;

string toupper(string S){
  for(char &c: S) c += 'A' - 'a';
  return S;
}

int main(){
  string S;
  cin >> S;
  cout << toupper(S) << endl;
}
```
::::

::::details こちらも良いです
```cpp
#include<bits/stdc++.h>
using namespace std;

string toupper(string S){
  for(char &c: S) c = toupper(c);
  return S;
}

int main(){
  string S;
  cin >> S;
  cout << toupper(S) << endl;
}
```
::::
