>题目

将两个有序链表进行融合，返回新链表的头部；

- 实现

（1）cur1:链表1 cur2:链表2 pre:在两个链表中来回移动，用于融合过程

（2）cur1:链表头较小 cur2：链表头较大

（3）更新过程，pre指向较小值，较小值指向较大值，较小值赋值给pre，较小值使用next更新自己

```
package Chapter2;

/**
 * @author Ethan
 * @desc 实现有序链表合并 
 */
public class C2Merge {
	
	public Node merge(Node head1,Node head2){
		//一个链表为空，返回另一个链表
		if(head1 == null || head2 == null){
			return head1 == null ? head2 : head1;
		}
		//以头节点小的链表头作为最终链表的头节点
		Node head = head1.value < head2.value ? head1 : head2;
		Node cur1 = head == head1 ? head1 : head2;
		Node cur2 = head == head1 ? head2 : head1;
		Node pre = null;
		Node next = null;
		
		while(cur1 != null && cur2 != null){
			if(cur1.value <= cur2.value){
				pre = cur1;
				cur1 = cur1.next;
			}else{
				next = cur2.next;
				pre.next = cur2;
				cur2.next = cur1;
				pre = cur2;
				cur2 = next;
			}
		}
		pre.next = cur1 == null ? cur2 : cur1;
		return head;
	}
}

```
