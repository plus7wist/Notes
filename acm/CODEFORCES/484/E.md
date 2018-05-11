---
title: #CODEFORCES 484E Sign on Fence
grammar_mathjax: true
---

## 链接

http://codeforces.com/contest/484/problem/E

## 题意

给出 n 个宽度为 1 ，高度为 h[i] 的矩形，从 1 到 n 连续挨着排。有 m 次询问，每次询问一段区间 [l, r] 中组成宽度为 w 的矩形的最高高度是多少？(n, m &le; 1e5, h[i] &le; 1e9)

## 思路

自己没想到。听子卿讲题解。

### 二分答案

二分答案 h，判定 [l, r] 内不低于 h 的矩形是否有连续 w 个。

对于固定 h 的判定问题，我们只要建立一颗线段树，区间存内部大于等于 h 的最长区间长度，靠左靠右的最长区间长度还有本区间长度，进行区间合并。查询 [l, r] 最长连续长度，如果大于等于 w 那么判断就通过。

### 可持久化

有了上述分析，这个问题要解决的话，只要把对应每个高度的线段树都建立出来就可以了。但是一颗一颗建立显然是不允许的。

注意到线段树之间有共用关系，比如数据是：1 2 2 3。如果对应高度 3 建立了线段树，那么高度为 2 对应的线段树可以看做是高度 3 的线段树进行单点更新（两次）的结果。

如此一来，我们可以将线段树可持久化，解决线段树的建立问题。

复杂度容易知道是：`!$O(m\log^2(n))$`，可以通过该题。

## 错误

我昨晚写这个题的时候犯了个错误，导致一直没过。

错误主要原因是建树出错，从前建树为了节省时间和内存，函数式的起始树我不会完整的建立，而是用一个点代替，所有要访问这个起始树的都访问到这一个节点。一般这个节点的标号是 0，左右儿子的标号也是 0。起始树当然标记成 root[0] = 0。

但是没有深刻的认识到这个技巧只能用于空树的所有节点的值都相同的状况。对于这个题目，因为我对每个点存了本区间长度，所以是不能这样用的。

## 代码

```cpp?linenums
// c head files
#include <stdio.h>
#include <assert.h>
// c++ head files
#include <algorithm>
using std::max;
using std::sort;
using std::unique;
#include <iostream>
using std::cout;
using std::endl;

const int MAXN = 100000 + 5;
const int LOG = 20;
const int MAXT = LOG * MAXN;

namespace FST
{
  struct TNode
  {
    int len;
    int lenL;
    int lenR;
    int lenMax;

    int lson;
    int rson;
  } tree[MAXT];

  int nodeCnt = 0;

  typedef TNode& ref;
  typedef const ref cref;

  void push(cref l, cref r, ref now)
  {
    now.len = l.len + r.len;
    now.lenMax = max(max(l.lenMax, r.lenMax), l.lenR + r.lenL);
    now.lenL = l.lenL + (l.lenL == l.len ? r.lenL : 0);
    now.lenR = r.lenR + (r.lenR == r.len ? l.lenR : 0);
  }

  void push(ref now)
  {
    int l = now.lson;
    int r = now.rson;
    push(tree[l], tree[r], now);
  }

  void init(int& now, int l, int r)
  {
    now = nodeCnt++;
    if (l == r) {
      tree[now].len = 1;
      tree[now].lenL = 0;
      tree[now].lenR = 0;
      tree[now].lenMax = 0;
      return;
    }
    int mid = (l + r) >> 1;
    init(tree[now].lson, l, mid);
    init(tree[now].rson, mid + 1, r);
    push(tree[now]);
  }

  void init(int n, int& root0)
  {
    nodeCnt = 0;
    init(root0, 1, n);
  }

  void update(int& now, int l, int r, int i)
  {
    tree[nodeCnt] = tree[now];
    now = nodeCnt++;
    assert(nodeCnt < MAXT);
    if (l == r) {
      tree[now].len = 1;
      tree[now].lenL = 1;
      tree[now].lenR = 1;
      tree[now].lenMax = 1;
      return;
    }
    int mid = (l + r) >> 1;
    if (i <= mid)
      update(tree[now].lson, l, mid, i);
    else update(tree[now].rson, mid + 1, r, i);
    push(tree[now]);
    assert(tree[now].len == (r - l + 1));
  }

  TNode query(int now, int l, int r, int ql, int qr)
  {
    if (ql == l && qr == r)
      return tree[now];
    int mid = (l + r) >> 1;
    if (qr <= mid)
      return query(tree[now].lson, l, mid, ql, qr);
    if (ql > mid)
      return query(tree[now].rson, mid + 1, r, ql, qr);

    TNode lson, rson, result;
    lson = query(tree[now].lson, l, mid, ql, mid);
    rson = query(tree[now].rson, mid + 1, r, mid + 1, qr);
    push(lson, rson, result);
    return result;
  }

  int query(int now, int n, int ql, int qr)
  {
    return query(now, 1, n, ql, qr).lenMax;
  }
}

using FST::query;
using FST::update;
using FST::init;

struct Node
{
  int value;
  int index;
} a[MAXN];

int value[MAXN];
int root[MAXN];

bool cmp(const Node& a, const Node& b)
{
  return a.value < b.value;
}

int main()
{
#ifndef ONLINE_JUDGE
  freopen("data.in", "r", stdin);
#endif // ONLINE_JUDGE
  int n;
  int cnt;
  scanf("%d", &n);
  for (int i = 1; i <= n; i++) {
    scanf("%d", &a[i].value);
    a[i].index = i;
    value[i] = a[i].value;
  }
  sort(a + 1, a + n + 1, cmp);
  sort(value + 1, value + n + 1);
  cnt = unique(value + 1, value + n + 1) - (value + 1);
  init(n, root[0]);
  for (int i = cnt, j = n; i >= 1; i--) {
    root[i] = root[(i + 1) % (cnt + 1)];
    for (; j >= 1 && a[j].value == value[i]; j--)
      update(root[i], 1, n, a[j].index);
  }

  int m;
  int l, r, w;
  int low, upp, mid;
  scanf("%d", &m);
  for (; m--; ) {
    scanf("%d %d %d", &l, &r, &w);
    low = 0;
    upp = cnt + 1;
    // [low, upp)
    for (; upp - low > 1; ) {
      mid = (low + upp) >> 1;
      if (query(root[mid], n, l, r) >= w)
        low = mid;
      else upp = mid;
    }
    printf("%d\n", value[low]);
  }
  return 0;
}
```