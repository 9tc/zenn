---
title: "ABC292-B: Yellow and Red Card č§ŖčĒŦ"
emoji: "đ˛"
type: "tech" # tech: æčĄč¨äē / idea: ãĸã¤ããĸ
topics: [AtCoder]
published: true
---

## åéĄ(åéĄčĒ­č§Ŗããã¨ãããĒãã¨ãč¨ãŖãĻãžã)
> $N$äēēããĻīŧãããããŽäēēã¯0ãã¤ãŗãæãŖãĻãžã
> $Q$å$c$ã¨$x$ãåãåãå¯žčŠąããžã
>   $c$ã1ãããã¯2ãĒãã°īŧäēē$x$ãŽãã¤ãŗãã$c$ãã¤ãŗãåĸãããžã
>   $c$ã3ãĒãã°īŧäēē$x$ãŽãã¤ãŗãã$2$äģĨä¸ããŠããį­ããĻãã ãã

### åļį´
> $1 \leq N \leq 100$
> $1 \leq Q \leq 100$
> $1 \leq x \leq N$

https://atcoder.jp/contests/abc292/tasks/abc292_b

## č§ŖčĒŦ
- æį´ãĢããã ã
- åéĄæãéˇããīŧãããã¨ã¯ãˇãŗããĢ
  - éåã§ãã¤ãŗããįŽĄįããĻãããã°č¯ã

::::details ãŗãŧã
```cpp
#include<bits/stdc++.h>
using namespace std;

int main(){
  int N, Q;
  cin >> N >> Q;

  vector<int> point(N, 0);
  while(Q--){
    int c, x;
    cin >> c >> x;
    if(c == 1 || c == 2) point[x-1] += c;
    if(c == 3){
      if(point[x-1] >= 2) cout << "Yes" << endl;
      else cout << "No" << endl;
    }
  }
}
```
::::
https://atcoder.jp/contests/abc292/submissions/39461742
