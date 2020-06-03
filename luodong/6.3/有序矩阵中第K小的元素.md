# [378. 有序矩阵中第K小的元素(https://leetcode-cn.com/problems/kth-smallest-element-in-a-sorted-matrix/)


> 解题思路分析

-  使用优先级队列，大顶堆解决


### 代码实现


~~~java
class Solution {
    public int kthSmallest(int[][] matrix, int k) {
        //转换为大顶堆
        PriorityQueue<Integer> queue = new PriorityQueue<>(new Comparator<Integer>() {
            @Override
            public int compare(Integer o1, Integer o2) {
                return o2.compareTo(o1);
            }
        });
        for(int i=0;i<matrix.length;i++){
            for(int j=0;j<matrix[0].length;j++){
                queue.offer(matrix[i][j]);
                //大于K就移除
                if(queue.size()>k){
                    queue.poll();
                }
            }
        }
        return queue.peek();
    }

}
~~~