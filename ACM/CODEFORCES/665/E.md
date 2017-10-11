---
garmmar_sup: true
---

<http://codeforces.com/contest/665/problem/E>

给出 n 个整数 a[1], a[2], ..., a[n]。 问有多少区间的亦或和大于等于 k。

## Input

n k
a[1] a[2] ... a[n]

1 &le; n &le; 1e6
1 &le; k &le; 1e9
0 &le; a[i] &le; 1e9

## Output

亦或和大于等于 k 的区间个数。

## Examples

Case 1
```
3 1
1 2 3
```
```
5
```
Case 2
```
3 2
1 2 3
```
```
3
```
Case 3
```
3 3
1 2 3
```
```
2
```

## Solution

处理前缀亦或和 s[i]。转化选择两个数 s[i] 和 s[j] （0 <= i < j <= n），使得 s[i] ^ s[j] >= k。这是个经典问题，使用将每个数看做是 31 位比特串（最高位看做第一个字符）。 对于每个 i，所有 s[j]（0 <= j < i）插入到字典树中。字典树每个节点还要记录经过该点的字符串的数目。

如此一来我们考查 s[j] 和 k，如果第 i 位有 2^i^ >= k，那么，如果选择与 s[j] 的第 i 位不相同的位，那么亦或的结果中就有 2^i^，也就是说一定满足要求，故上述方向上字典树里的单词数目应该全部加到答案上，字典树上只需走相反的方法再计算；反之，如果 2^i^ < k，如果选择与 s[j] 的 第 i 相同的位，当前位的亦或为 0，后面即使全部都是 1 也不会比 2^i^ 大，故肯定是不能让总亦或值大于等于 k，所以一定要走另外的方向，并且使得 k -= 2^i^。

综上，字典树的每一层只走一个点。当然，计数完 s[j] 之后要将 s[j] 插入字典树，以便判断下一个数。总之，可以在 O(nlog(n)) 的时间内通过本题。

## Code

```cpp?linenums
#include <stdio.h>
#include <string.h>

#include <vector>

const int N = 1000000 + 100;

int a[N];

struct trie_t
{
#define each_bit(i) for (int i = 30; i >= 0; --i)

  struct node
  {
    int nxt[2];
    int cnt;

    node()
    {
      cnt = 0;
      nxt[0] = nxt[1] = -1;
    }
  };

  std::vector<node> v;

  void init()
  {
    // v.clear();
    v.push_back(node());
  }

  void insert(int x)
  {
    int now = 0;
    v[0].cnt++;
    each_bit(i) {
      int b = ((x >> i) & 1);
      if (v[now].nxt[b] == -1) {
        v[now].nxt[b] = v.size();
        v.push_back(node());
      }
      now = v[now].nxt[b];
      v[now].cnt++;
    }
  }

  int count(int x, int k)
  {
    int now = 0;
    int ans = 0;
    each_bit(i) {
      int b = ((x >> i) & 1);
      if ((1 << i) >= k) {
        // numbers via nxt[!b] are big enough
        if (v[now].nxt[!b] != -1) {
          ans += v[v[now].nxt[!b]].cnt;
        }
        now = v[now].nxt[b];
      }
      else { // (1 << i) < k
        // numbers via nxt[b] are too small
        now = v[now].nxt[!b];
        k -= (1 << i);
      }
      if (now == -1) {
        break;
      }
    }
    return ans;
  }
#undef each_bit
} trie;

int main()
{
  int n, k;
  scanf("%d %d", &n, &k);
  for (int i = 1; i <= n; ++i) {
    scanf("%d", a+i);
    a[i] ^= a[i-1];
  }

  long long ans = 0;
  trie.init();
  for (int i = 0; i <= n; ++i) {
    ans += trie.count(a[i], k);
    trie.insert(a[i]);
  }
  printf("%I64d\n", ans);
  return 0;
}
```
