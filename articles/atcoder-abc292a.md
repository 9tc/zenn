---
title: "ABC292-A: CAPS LOCK è§£èª¬"
emoji: "ð²"
type: "tech" # tech: æè¡è¨äº / idea: ã¢ã¤ãã¢
topics: [AtCoder]
published: true
---

## åé¡(æ¦è¦)
> è±å°æå­ãããªãæå­å$S$ãä¸ããããã®ã§ï¼å¨ã¦å¤§æå­ã«ãã¦åºåãã¦ãã ãã

### å¶ç´
> $1 \leq |S| \leq 100$

https://atcoder.jp/contests/abc292/tasks/abc292_a

## è§£èª¬
- å¤§æå­ã«å¤æããé¢æ°(C++ã ã¨toupperé¢æ°)ãä½¿ãã¨ä¾¿å©
- ASCIIã³ã¼ããç´æ¥æ±ããã¨ã«æ£ããã¨è¯ã
  - charåãæ°ã¨ã¿ã¦è¶³ãããå¼ãããããã¨æå­ã®å¤æãã§ãã
    - 'A' + 1 -> 'B'ã¿ãããª
  - ä»åã¯å°æå­ãå¤§æå­ã«å¤æããã®ã§ï¼åæå­ã«'A' - 'a'ãè¶³ãã¦ãããã°å¤§æå­ã«ãªã

::::details ã³ã¼ã
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

::::details ããããã®ã¯é¢æ°ã«åãã¦ããããã¿ãããã§ã
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

::::details ãã¡ããè¯ãã§ã
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
