// CODEFORCES 645E Intellectual Inquiry

<http://codeforces.com/problemset/problem/645/E>

字母表只有前面 k 个小写字母。给出一个字符串 s，你可以往 s 后添加 n 个字母，使得，总的字符串的不同子序列最多。

## Input

	n k
	s

1 &le; n &le; 1,000,000
1 &le; k &le; 26
1 &le; |s| &le; 1,000,000

## Output

输出答案模 1,000,000,007。

## Solution

看了题解才会的。

f[i] 表示以 i 为结尾的子序列（不含空串）有多少个，往字符串后面加一个字母 c，则只有 f[c] 会改变。而且是改成 &sum;f[] + 1。重点在这个值跟 c 是没有关系的，改变之后的所以子序列数目的和是 &sum;f[] - f[c] + &sum;f[] + 1，要使这个值最大，应该使得 f[c] 最小，也就是说，添加一个使得 f[c] 最小的 c 在字符串末尾是最佳的方案。

## Code

```cpp?linenums
/**
 * Author: +7w
 */
#include <assert.h>
#include <ctype.h>
#include <inttypes.h>
#include <math.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>

#include <algorithm>
#include <bitset>
#include <functional>
#include <list>
#include <iostream>
#include <map>
#include <queue>
#include <set>
#include <stack>
#include <sstream>
#include <string>
#include <vector>

const int INF3 = 0x3f3f3f3f;
const int INF5 = 0x5f5f5f5f;
const double PI = acos(-1.0);
const double EPS9 = 1e-9;
const int TEN3 = 1000;
const int TEN6 = TEN3 * TEN3;
const int TEN9 = TEN6 * TEN3;

typedef long long llong;
typedef unsigned long long ullong;
typedef std::pair<int, int> pii;

#define FST first
#define SEC second
#define PB push_back
#define MP make_pair
#define CLEAR(a) memset(a, 0, sizeof(a))
#define FILL(a, c) memset(a, c, sizeof(a))
#define COPY(a, b) memcpy(a, b, sizeof(b))

const int MOD = TEN9 + 7;
const int N = TEN6 + 10;
const int K = 30;
const int M = TEN6 + 10;

char str[M];
pii cv[N];

int main(int argc, char const *argv[])
{
  int n, k;
  scanf("%d %d", &n, &k);
  scanf("%s", str);
  for (int i = 0; i < k; ++i) {
    cv[i].FST = i; // cmper
    cv[i].SEC = 0; // value
  }
  int sum = 0;
  for (int i = 0; str[i]; ++i) {
    int j = str[i] - 'a';
    int tmp_sec = cv[j].SEC;
    cv[j].SEC = (sum + 1) % MOD;
    sum = (sum - tmp_sec + MOD) % MOD;
    sum = (sum + cv[j].SEC) % MOD;
    cv[j].FST = i + k;
  }
  std::sort(cv, cv + k);
  for (int i = 0; i < n; ++i) {
    int j = i % k;
    int tmp_sec = cv[j].SEC;
    cv[j].SEC = (sum + 1) % MOD;
    sum = (sum - tmp_sec + MOD) % MOD;
    sum = (sum + cv[j].SEC) % MOD;
  }
  printf("%d\n", (sum + 1) % MOD);
  return 0;
}
```
