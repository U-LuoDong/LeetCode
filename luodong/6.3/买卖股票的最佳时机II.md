# [122. 买卖股票的最佳时机 II](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii/)


> 解题思路分析

-  思路：二维DP动态规划
-  状态：第i天，交易次数，是否持有股票
-  选择：在买、卖和等待之中选择最大值


### 代码实现


~~~java
//法一
class Solution {
    public int maxProfit(int[] prices) {
        int n = prices.length;
        if(n==0)
            return 0;
        int[][] dp = new int[n][2];
        //初始化dp数组:第一天持有或未持有股票
        dp[0][1] = -prices[0];
        dp[0][0] = 0;
        //从第二天开始
        for(int i=1;i<n;i++){
            dp[i][0] = Math.max(dp[i-1][0],dp[i-1][1]+prices[i]);
            dp[i][1] = Math.max(dp[i-1][1],dp[i-1][0]-prices[i]);
        }
        return dp[n-1][0];
    }
}
法二：优化
class Solution {
    public int maxProfit(int[] prices) {
        //思路：二维DP动态规划
        //状态：第i天，交易次数，是否持有股票
        //选择：在买、卖和等待之中选择最大值
        int n = prices.length;
        if(n==0)
            return 0;
        //初始化dp数组:第一天持有或未持有股票
        int dp_1 = -prices[0];
        int dp_0 = 0;
        //从第二天开始
        for(int i=1;i<n;i++){
            int tmp = dp_0;
            dp_0 = Math.max(dp_0,dp_1+prices[i]);
            dp_1 = Math.max(dp_1,tmp-prices[i]);
        }
        return dp_0;
    }
}
~~~