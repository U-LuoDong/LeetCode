# [1306. 跳跃游戏 III](https://leetcode-cn.com/problems/jump-game-iii/)


> 解题思路分析

-  广度优先：队列+标记数组【不用节点进行记录】


### 代码实现


~~~java
class Solution {
    public boolean canReach(int[] arr, int start) {
        if(arr[start] == 0)
            return true;
        int[] map = new int[arr.length];
        Queue<Integer> queue = new LinkedList<Integer>();
        queue.add(start);
        map[start]=1;
        while(queue.size()!=0){
            int cur = queue.poll();
            if(cur+arr[cur]<arr.length && map[cur+arr[cur]]!=1){
                if(arr[cur+arr[cur]] == 0)
                    return true;
                queue.add(cur+arr[cur]);
                map[cur+arr[cur]] =1;
            }
            if(cur-arr[cur]>=0 && map[cur-arr[cur]]!=1){
                if(arr[cur-arr[cur]] == 0)
                    return true;
                queue.add(cur-arr[cur]);
                map[cur-arr[cur]] =1;
            }
        }
        return false;
    }
}
~~~