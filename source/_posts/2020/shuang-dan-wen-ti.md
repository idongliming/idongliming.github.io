---
title: 双蛋问题
date: 2020-03-12 20:25:49
categories: "算法和数据结构"
tags:
    - leetcode
    - 二分法
    - 动态规划
keywords: 
    - 双蛋问题
    - leetcode
top:
cover:
summary:
password:
mathjax:
---

## 参考视频

李永乐老师的视频,讲的很通俗易懂了，下面做一下leetcode对应的题

<iframe width="830" height="515" src="https://www.youtube.com/embed/mLV_vOet0ss" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## 题目描述

这是leetcode 第 887 题 [鸡蛋掉落](https://leetcode-cn.com/problems/super-egg-drop/)

> 你将获得 K 个鸡蛋，并可以使用一栋从 1 到 N  共有 N 层楼的建筑。
每个蛋的功能都是一样的，如果一个蛋碎了，你就不能再把它掉下去。
你知道存在楼层 F ，满足 0 <= F <= N 任何从高于 F 的楼层落下的鸡蛋都会碎，从 F 楼层或比它低的楼层落下的鸡蛋都不会破。
每次移动，你可以取一个鸡蛋（如果你有完整的鸡蛋）并把它从任一楼层 X 扔下（满足 1 <= X <= N）。
你的目标是确切地知道 F 的值是多少。
无论 F 的初始值如何，你确定 F 的值的最小移动次数是多少？

示例 1

```
输入：K = 1, N = 2
输出：2
解释：
鸡蛋从 1 楼掉落。如果它碎了，我们肯定知道 F = 0 。
否则，鸡蛋从 2 楼掉落。如果它碎了，我们肯定知道 F = 1 。
如果它没碎，那么我们肯定知道 F = 2 。
因此，在最坏的情况下我们需要移动 2 次以确定 F 是多少。

```

示例 2

```
输入：K = 2, N = 6
输出：3
```

示例 3 

```
输入：K = 3, N = 14
输出：4
```


## 解题思路

- 穷举法

- 二分法

- 动态规划

### 穷举法

最简单的方法就是一层一层试验，这样只需要一个鸡蛋就可以了。

### 二分法

使用二分查找，例如，第一个鸡蛋再50层扔下，如果碎了，第二个鸡蛋从1-49逐层试验；如果没碎，第一个鸡蛋在75层扔下，如果碎了，第二个鸡蛋从51-74逐层试验…但是，这个方法，很容易悲剧，例如，当正好49层是可以安全落下的，需要尝试50次。比只有一个鸡蛋的情况，效果还要差。

### 动态规划

采用动态规划的方法，最重要的是要找到子问题。做如下的分析，假设f{n}表示从第n层楼扔下鸡蛋，没有摔碎的最少尝试次数。第一个鸡蛋，可能的落下位置(1,n),第一个鸡蛋从第i层扔下，有两个情况：

* 碎了，第二个鸡蛋，需要从第一层开始试验，有i-1次机会

* 没碎，两个鸡蛋，还有n-i层。这个就是子问题了f{n-i}

所以，当第一个鸡蛋，由第i个位置落下的时候，要尝试的次数为1 + max(i - 1, f{n - i})，那么对于每一个i，尝试次数最少的，就是f{n}的值。状态转移方程如下：
f{n} = min(1 + max(i - 1, f{n - 1}) ) 其中: i的范围为(1, n), f{1} = 1

## 代码

- 二分法

```java
class Solution {
    public int superEggDrop(int K, int N) {
        return dp(K, N);
    }

    Map<Integer, Integer> memo = new HashMap();
    public int dp(int K, int N) {
        if (!memo.containsKey(N * 100 + K)) {
            int ans;
            if (N == 0)
                ans = 0;
            else if (K == 1)
                ans = N;
            else {
                int lo = 1, hi = N;
                while (lo + 1 < hi) {
                    int x = (lo + hi) / 2;
                    int t1 = dp(K-1, x-1);
                    int t2 = dp(K, N-x);

                    if (t1 < t2)
                        lo = x;
                    else if (t1 > t2)
                        hi = x;
                    else
                        lo = hi = x;
                }

                ans = 1 + Math.min(Math.max(dp(K-1, lo-1), dp(K, N-lo)),
                                   Math.max(dp(K-1, hi-1), dp(K, N-hi)));
            }

            memo.put(N * 100 + K, ans);
        }

        return memo.get(N * 100 + K);
    }
}

```

- 动态规划

```java
class Solution {
    public int superEggDrop(int K, int N) {
        // Right now, dp[i] represents dp(1, i)
        int[] dp = new int[N+1];
        for (int i = 0; i <= N; ++i)
            dp[i] = i;

        for (int k = 2; k <= K; ++k) {
            // Now, we will develop dp2[i] = dp(k, i)
            int[] dp2 = new int[N+1];
            int x = 1;
            for (int n = 1; n <= N; ++n) {
                // Let's find dp2[n] = dp(k, n)
                // Increase our optimal x while we can make our answer better.
                // Notice max(dp[x-1], dp2[n-x]) > max(dp[x], dp2[n-x-1])
                // is simply max(T1(x-1), T2(x-1)) > max(T1(x), T2(x)).
                while (x < n && Math.max(dp[x-1], dp2[n-x]) > Math.max(dp[x], dp2[n-x-1]))
                    x++;

                // The final answer happens at this x.
                dp2[n] = 1 + Math.max(dp[x-1], dp2[n-x]);
            }

            dp = dp2;
        }

        return dp[N];
    }
}

```

## 小结

leetcode hard 看科普视频看懂了，实际做 leetcode 动态规划还有欠缺，下一步重点理解动态规划
