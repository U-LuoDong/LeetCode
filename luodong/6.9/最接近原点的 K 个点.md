# [973. 最接近原点的 K 个点](https://leetcode-cn.com/problems/k-closest-points-to-origin/)


> 解题思路分析

-  创建一个距离数组，然后排序找到第 K 大的距离，然后返回距离小于等于这个第 K 大距离的 K 个点



### 代码实现


~~~java
class Solution {
    public int[][] kClosest(int[][] points, int K) {
        int N = points.length;
        int[] dists = new int[N];
        for (int i = 0; i < N; ++i)
            dists[i] = dist(points[i]);

        Arrays.sort(dists);
        int distK = dists[K-1];

        int[][] ans = new int[K][2];
        int t = 0;
        for (int i = 0; i < N; ++i)
            if (dist(points[i]) <= distK)
                ans[t++] = points[i];
        return ans;
    }

    public int dist(int[] point) {
        return point[0] * point[0] + point[1] * point[1];
    }
}
~~~