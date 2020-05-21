557. 反转字符串中的单词 III
~~~java
class Solution {
    public String reverseWords(String s) {
        s = s.trim();
        char[] arr = s.toCharArray();
        char[] keep = new char[arr.length];
        Stack<Integer> stack = new Stack<>();
        stack.push(arr.length);
        for(int i = arr.length-1; i >= 0; i--) {
            if (arr[i] == ' ') {
                stack.push(i);
            }
        }

        int keepIndex = stack.pop();
        for(int i = 0; i < arr.length; i++) {
            if (arr[i] == ' ') {
                keep[i] = arr[i];
                keepIndex = stack.pop();
            } else {
                keep[--keepIndex] = arr[i];
            }
        }
        return new String(keep);
    }
}
~~~

54. 螺旋矩阵
~~~java
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        if (matrix == null || matrix.length <= 0) {
            return new ArrayList<>();
        }
        int length = matrix.length * matrix[0].length;
        List<Integer> list = new ArrayList<>(length);
        int left = 0;
        int right = matrix[0].length - 1;
        int top = 0;
        int bottom = matrix.length - 1;
        while(list.size() <= length) {
            for(int i = left; i <= right; i++) {
                list.add(matrix[top][i]);
            }
            top++;
            if (length == list.size()) {
                break;
            }
            for(int i = top; i <= bottom; i++) {
                list.add(matrix[i][right]);
            }
            right--;
            if (length == list.size()) {
                break;
            }
            for(int i = right; i >= left; i--) {
                list.add(matrix[bottom][i]);
            }
            bottom--;
            if (length == list.size()) {
                break;
            }
            for(int i = bottom; i >= top; i--) {
                list.add(matrix[i][left]);
            }
            left++;
        }
        return list;
    }
}
~~~


920. 播放列表的数量
~~~java
class Solution {
    public int numMusicPlaylists(int N, int L, int K) {
        long[][] dp = new long[L+1][N+1];
        dp[0][0] = 1;
        for(int i = 1; i < dp.length; i++) {
            for(int j = 1; j < dp[i].length; j++) {
                dp[i][j] += dp[i-1][j-1]*(N-j+1);
                dp[i][j] %= (1e9+7);
                if (j > K) {
                    dp[i][j] += dp[i-1][j]*(j-K);
                    dp[i][j] %= (1e9+7);
                }
                
            }
        }
        return (int)dp[L][N];
    }
}
~~~
