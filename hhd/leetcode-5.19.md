9. 回文数
~~~java
class Solution {
    public boolean isPalindrome(int x) {
        if(x < 0) {
            return false;
        }
        int pow = 1;
        while(x/pow >= 10) {
            pow *= 10;
        }
        while(x > 0) {
            int high = x/pow;
            int low = x%10;
            if (high != low) {
                return false;
            }
            x %= pow;
            x /= 10;
            pow /= 100;
        }
        return true;
    }
}
~~~


5. 最长回文子串
~~~java
class Solution {
    public String longestPalindrome(String s) {
        if (s == null || s.length() <= 1) {
            return s;
        }
        int keepL = 0;
        int keepR = 0;
        boolean[][] dp = new boolean[s.length()][s.length()];
        for(int r = 1; r < s.length(); r++) {
            for(int l = 0; l < r; l++) {
               if ((s.charAt(l)==s.charAt(r))&&(r-l<=2 || dp[l+1][r-1])) {
                    dp[l][r] = true;
                    if (r-l > keepR-keepL) {
                        keepL = l;
                        keepR = r;
                    }
               }
            }
        }
        return s.substring(keepL,keepR+1);
    }
}
~~~

124. 二叉树中的最大路径和
~~~java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {

    Integer maxVal = Integer.MIN_VALUE;

    public int maxPathSum(TreeNode root) {
        if (root == null) {
            return 0;
        }
        dfs(root);
        return maxVal;
    }

    public int dfs(TreeNode node) {
        if (node == null) {
            return 0;
        }
        int leftValue = 0;
        int rightValue = 0; 
        leftValue = Math.max(0, dfs(node.left));
        rightValue = Math.max(0, dfs(node.right));
        int temp = node.val + leftValue + rightValue;
        int res = node.val + Math.max(leftValue, rightValue);
        maxVal = Math.max(maxVal, temp);
        return res;
    }
}
~~~
