# 十题（一）

---

## CF707D Persistent Bookcase

n &times; m 的网格，每个位置是 0 或者 1，四种操作：

- (1, x, y)：(x, y) 处的网格如果是 0，则变为 1。
- (2, x, y)：(x, y) 处的网格如果是 1，则变为 0。
- (3, x)：把第 x 行的所有数字取反。
- (4, k)：整个状态回退到第 k 个操作之后

每个操作之后都输出当前网格中数字的和。n, m &le; 1000，至多 1e5 组操作。

如果没有第四个操作，只要记录每个位置是多少，标记每一行是否取反，记录每一行的和，记录总和，就可以相互 O(1) 的维护。对于第四种操作，考虑离线，按照询问后状态的依赖建立图，按照 dfs 顺序求解答案即可。

## CF118C Fancy Number

给出一个最长 1000 的十进制数字，要使得至少有某个数码出现至少 m 次，有可能需要更改某些位置的数码，改动数码的代价就是数码之间差的绝对值。问总共至少要多少代价即可做到这一点。并且输出修改后的结果，如果有多种相同代价的结果，输出字典顺序最小的一个。

枚举出现至少 m 次的数码。

## CF264C Choosing Balls

每个球有个颜色和对应的价值，给出一对参数 (a,b)，定义一个球序列的价值：如果一个球跟它前面的球的颜色一样，那么这个球对序列价值的贡献是 a &times; 球的价值；如果颜色不同（或者当前就是第一个球），那么贡献是 b &times; 球的价值。

给出一个球的序列，要你选出一个子序列，使得子序列的价值最大。数据共用一组球序列（最多 100000 个球），但分成 q 组查询（最多 500 组），每组使用不同的 (a,b)，要输出最大价值。

用 f[c] 表示最后一个球颜色是 c 的子序列的最大价值。自左向右更新 f，对于当前的球，设颜色是 ci，价值是 vi。那么拟计算以当前球为结尾的子序列的最大价值 V。V 即是 a &times; vi + f[ci] 和 max(b &times; vi + f[cj]): ci &ne; cj。后者也就是 b &times; vi + max(f[cj]): ci &ne; cj。求 max 的部分是这个题的关键，使用线段树或者树状数组（两个）好像都是要 TLE 的。可以考虑，保存最大 f 对应的颜色 maxc，和次大颜色的 maxc2，维护这两个值就可以得到 max(..)。

## CF498C Array and Operations

给出 100 个正整数（不超过 1e9），给出 m 对下标 (i,j)，每对 (i,j) 满足 i+j 是一个奇数。拟对这 n 个数进行操作，每次可以选择一对给出的下标，将对应的两个数除以某个公约数（须得大于一）。问最多可以进行多少次操作。

由于 i 和 j 必然一奇一偶，我们可以将奇数和偶数分开。将每个数字分解成素数簇，每簇建立一个点，对于偶数下标到奇数下标，相同素数簇基的点建立一条边，边权是两个簇指数的最小值。并且，建立源点，到每个偶数部分点建立边；建立汇点，每个奇数部分点到汇点建立边，边权即指数大小。如此一来，源点到汇点的最大流即是最多可进行的操作数。

标解是二分图匹配，暂时不懂。

## CF145B Lucky Number 2

问最小的，满足给定的 4、7、47、74 子串数目的数是几。不存在输出 -1。（1 &le; ... &le; 1e6）

考虑到 abs(cnt47 - cnt74) 不会超过 2，按照这个值取 -1，0，1 讨论，先考虑只有 47 相间的情况（4 开头或者 7 开头等等……），再将剩余的 4 和 7 插入。4 尽量往前插，7 尽量往后插。
