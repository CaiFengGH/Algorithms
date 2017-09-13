>题目描述

两个整型数字，以逆序链表的形式给出，求两个数的和，并以逆序的形式给出；

1-2-3 和 4-5-6-7，即321和7654相加；

```
public class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        //初始化返回结果
        ListNode res = new ListNode(0);
        ListNode current = res;
        //记录两个链表的当前节点
        ListNode current1 = l1;
        ListNode current2 = l2;
        //记录进位
        int carry = 0;
        int sum = 0;
        //循环实现加法
        while(current1 != null || current2 != null){
            int x = (current1 != null) ? current1.val : 0;
            int y = (current2 != null) ? current2.val : 0;
            sum = x + y + carry;
            carry = sum / 10;
            current.next = new ListNode(sum % 10);
            //更新current
            current = current.next;
            if(current1 != null) current1 = current1.next;
            if(current2 != null) current2 = current2.next;
        }
        if(carry > 0){
            current.next = new ListNode(carry);
        }
        //返回结果
        return res.next;
    }
}
class ListNode{
    int val = 0;
    ListNode next;
    ListNode(int val){
        this.val = val;
}
```

