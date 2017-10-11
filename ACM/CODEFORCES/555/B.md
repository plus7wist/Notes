---
title: CODEFORCES ROUND 310 (Div. 1) B. Case of Fugitive
---

## 题目描述

<http://codeforces.com/contest/555/problem/B>

有 n 个小岛，每个小岛都是线段形状的。从左到右第 i 座岛从 l[i] 点开始到 r[i] 点结束，岛和岛之间没有相交的地方。

Andrewid 可以建立 m 座桥，每座桥可以用最多一次。一座长度是 a 的桥可以连接其第 i 和第 i+1 座小岛的当且仅当存在 x，y 使得 l[i] ≤ x ≤ r[i] 且 l[i+1] ≤ y ≤ r[i+1] 且 y - x = a。

Andrewid 可以将所有小岛连接起来吗？如果可以的话，给出一种方案。

## 思路

第 i 到第 i+1 个岛，要链接起来，需要的桥的长度在区间 [ l[i+1]-r[i], r[i+1]-l[i] ] 内，这样的话，就转换成了典型的分配问题。我们重新描述一下题目。

有 m 个点，分配给 n-1 条线段，每个点只能分配给至多一条包含这个点的线段，问是否存在一种方案使得所有线段都分配到点？

这个问题的解决方案是贪心。这里仅说明算法：自左向右扫描点，扫描每个点时，维护所有未分配过点的，并且包含当前点的线段到一个集合 S 里，如果发现当前 S 空，那么可以跳过，否则当前点则分配给 S 中右端点最小的线段。

如果预先将线段按照左端点升序排序，那么 S 需要支持的操作是插入线段，删除右边端点最小的线段这两条。所以可以使用优先队列，并使得右边端点小的优先级高。

```cpp?linenums
#include <stdio.h>
#include <string.h>

#include <queue>
#include <vector>
#include <algorithm>

const int N = 200000 + 5;

long long left[N];
long long right[N];

struct segment_t
{
  long long left;
  long long right;
  int index;
} segment[N];

struct left_order
{
  bool operator() (const segment_t& first, const segment_t& second)
  { return first.left < second.left; }
};

struct right_order
{
  bool operator() (const segment_t& first, const segment_t& second)
  {
    if (first.right != second.right)
      return first.right > second.right;
    return first.index < second.index;
  }
};

struct bridge_t
{
  long long length;
  int index;
} bridge[N];

struct length_order
{
  bool operator() (const bridge_t& first, const bridge_t& second)
  { return first.length < second.length; }
};

int answer[N];

int main()
{
#ifndef ONLINE_JUDGE
  freopen("input.txt", "r", stdin);
//  freopen("input.txt", "w", stdout);
#endif // ONLINE_JUDGE
  int n, m;
  scanf("%d %d", &n, &m);
  for (int i = 1; i <= n; ++i) {
    scanf("%I64d %I64d", &left[i], &right[i]);
  }
  for (int i = 1; i <= m; ++i) {
    scanf("%I64d", &bridge[i].length);
    bridge[i].index = i;
  }
  for (int i = 1; i < n; ++i) {
    segment[i].left = left[i+1] - right[i];
    segment[i].right = right[i+1] - left[i];
    segment[i].index = i;
  }
  std::sort(segment+1, segment+n, left_order());
  std::sort(bridge+1, bridge+1+m, length_order());
  std::priority_queue<segment_t, std::vector<segment_t>, right_order> pq;
  int ptr = 0;
  int assigned_count = 0;
  for (int i = 1; i <= m; ++i) {
    for (; ptr < n && segment[ptr].left <= bridge[i].length; ptr++) {
      pq.push(segment[ptr]);
    }
    for (; !pq.empty() && pq.top().right < bridge[i].length; pq.pop());
    if (pq.empty()) {
      continue;
    }
    assigned_count += 1;
    answer[pq.top().index] = bridge[i].index;
    pq.pop();
  }
  if (assigned_count == n - 1) {
    puts("Yes");
    for (int i = 1; i < n; ++i) {
      printf("%d ", answer[i]);
    }
    printf("\n");
  }
  else puts("No");
  return 0;
}
```