# [142. 环形链表 II](https://leetcode-cn.com/problems/linked-list-cycle-ii/)


> 解题思路分析

-  快慢指针，当相遇时，慢指针从头开始，快慢指针一次走一步

### 代码实现


~~~java
public class Solution {
    public ListNode detectCycle(ListNode head) {
        //思路：快慢指针，当相遇时，慢指针从头开始，快慢指针一次走一步
        ListNode slow = head;
        ListNode fast = head;
        while(fast!=null && fast.next!=null){
            fast = fast.next.next;
            slow = slow.next;
            if(fast == slow)
                break;
        }
        if(fast == null || fast.next==null)
            return null;
        slow = head;
        while(slow != fast){
            slow = slow.next;
            fast = fast.next;
        }
        return slow;
    }
}
~~~