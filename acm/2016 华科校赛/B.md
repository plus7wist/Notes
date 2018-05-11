// 2016 华科校赛 B. And

<http://acm.hust.edu.cn/problem/show/1672>

## 题目描述

给出 a[1], ..., a[n]。查询 t[1], ... t[m]，问有多少 a[] 的子序列的按位与是 t[]。

## 输入

多组测试，EOF 结束。

```
n
a[]
m
t[]
```

1 ≤ n ≤ 1e6
1 ≤ m ≤ (1 << 20)
1 ≤ a[i] ≤ (1 << 20)
1 ≤ t[i] ≤ (1 << 20)

## 输出

输出一行，每组查询输出一个数，每个数后面一个空格。

## 来源

sheep

## 思路

先膜拜一会儿……【三分钟之后】好了开始讲题解。

用分治的思想解决。目的是对于给定的 a[]，处理出一个数组 ans[]。ans[i] 的值就是按位与是 i 的子序列的数目。

考查这个问题的输入和输出，我们建立这样一个分治模型：work(int cnt[LEN], int ans[LEN])。其中 cnt[] 是输入，ans[] 是输出。cnt[i] 表示 a[] 中有多少个 i；ans[i] 表示有多少子序列按位与结果是 i。LEN 是当前值区间的长度，也就是说当前的 wrok 解决的问题是 [0, LEN) 范围内的结果。

对一个取值区间 [0, 2L) 分析解，最后答案就是 [0, 1<<20) 的解。

我们发现较大的一半 [L, 2L) 是容易解决的，因为这里面的数最高位是1，要按位与结果是这里面的数，选择的数也一定得在这个范围内才行（选择了一个 [0, L) 内的数之后，按位与最高位就是 0 了）。所以这个部分可以递归使用 work 解决，具体方法是 work(cnt1[], ans1[])，cnt1[i]是 cnt[i + L]；ans1[i] 将是 ans[i + L]。

但是较小的一半是不容易解决的，对 i &isin; [0, L)，可以选择 [0, L) 中的数，也可以选择 [L, 2L) 中的，只要最高位的1被与掉了就可以。既然如此我们不妨考虑整体，不直接计算 ans[i]，而计算 ans[i] + ans[i + L]。这个值的意义就是，无视最高位是多少，按位与的结果的剩下的部分是i的子序列数目。无视最高位，只要把 cnt[i] 和 cnt[i + L] 也就是一样的数。调用的方法是 work(cnt2[], ans2[])，这里的 cnt2[i] = cnt[i] + cnt[i + L]，ans2[i] 就是 ans[i] + ans[i + L]。

分完这两部分，就可以解决 ans[] 的计算了，对于 i &isin; [L, 2L)，ans[i] = ans1[i - L]；对于 i &isin; [0, L)，ans[i] = ans2[i] - ans1[i]。

## 代码

```cpp
#include <stdio.h>
#include <string.h>

#include <algorithm>
#include <vector>

const int MAXL = (1 << 20);
const int MOD = (int) 1e9 + 7;

int add(int a, int b)
{
  int c = a + b;
  if (c >= MOD)
    c -= MOD;
  return c;
}

int sub(int a, int b)
{
  int c = a - b;
  if (c < 0)
    c += MOD;
  return c;
}

int mul(int a, int b)
{ return (long long) a * b % MOD; }

typedef std::vector<int> array;

int pow2[MAXL];

void work(const array& cnt, array& ans)
{
  if (cnt.size() == 1) {
    ans[0] = sub(pow2[cnt[0]], 1);
    return;
  }
  int d = (cnt.size() >> 1);
  array cnt1(d);
  array ans1(d);
  for (int i = 0; i < d; ++i)
    cnt1[i] = cnt[i + d];
  work(cnt1, ans1);
  array cnt2(d);
  array ans2(d);
  for (int i = 0; i < d; ++i)
    cnt2[i] = add(cnt[i], cnt[i + d]);
  work(cnt2, ans2);
  for (int i = 0; i < d; ++i) {
    ans[i] = sub(ans2[i], ans1[i]);
    ans[i + d] = ans1[i];
  }
}

int a[MAXL];

int main(int argc, const char* argv[])
{
  pow2[0] = 1;
  for (int i = 1; i < MAXL; ++i) {
    pow2[i] = add(pow2[i - 1], pow2[i - 1]);
  }
  int n, m;
  array cnt(MAXL);
  array ans(MAXL);
  for (; scanf("%d", &n) == 1; ) {
    std::fill(cnt.begin(), cnt.end(), 0);
    for (int i = 0; i < n; ++i) {
      scanf("%d", a+i);
      cnt[a[i]]++;
    }
    work(cnt, ans);
    scanf("%d", &m);
    for (int i = 0; i < m; ++i) {
      scanf("%d", a+i);
      printf("%d ", ans[a[i]]);
    }
    printf("\n");
  }
  return 0;
}
```

