```
package Test;

/**
 * @author Ethan
 * @desc 单链表归并排序 
 */
public class ListMergeSort {
	
	/**
	 * @author Ethan
	 * @desc 基于归并排序思想解决单链表排序
	 */
	public ListNode listMergeSort(ListNode head){
		//1-异常参数检测
		if(head == null || head.next == null){
			return head;
		}
		//2-获取中间节点
		ListNode mid = getMiddle(head);
//		System.out.println(mid.value);
		ListNode halfNext = mid.next;
		mid.next = null;
		
		//3-递归调用
		return listMerge(listMergeSort(head),listMergeSort(halfNext));
	}

	/**
	 * @author Ethan
	 * @desc 链表归并 
	 */
	private ListNode listMerge(ListNode a, ListNode b) {
		//1-初始化 dummy: cur:
		ListNode dummy = new ListNode(0);
		ListNode cur = dummy;
		//2-归并过程
		while(a != null && b != null){
			if(a.value <= b.value){
				cur.next = a;
				a = a.next;
			}else{
				cur.next = b;
				b = b.next;
			}
			cur = cur.next;
		}
		//3-链表尾部
		cur.next = (a == null) ? b : a;
		//4-返回链表头部
		return dummy.next;
	}

	/**
	 * @author Ethan
	 * @desc 基于快慢指针返回中间节点 
	 */
	private ListNode getMiddle(ListNode head) {
		//1-初始化快慢指针
		ListNode slow = head;
		ListNode fast = head;
		
		//2-快指针一次两步，慢指针一次一步
		while(fast.next != null && fast.next.next != null){
			slow = slow.next;
			fast = fast.next.next;
		}
		//3-返回慢指针
		return slow;
	}
	
	public static void main(String[] args) {
		ListMergeSort lms = new ListMergeSort();
		
		ListNode a = new ListNode(1);
		ListNode b = new ListNode(3);
		ListNode c = new ListNode(2);
		ListNode d = new ListNode(5);
		ListNode e = new ListNode(4);
		
		a.next = b;
		b.next = c;
		c.next = d;
		d.next = e;
		
		printList(a);
		System.out.println();
		
		lms.listMergeSort(a);
		
		printList(a);
	}

	private static void printList(ListNode head) {
		ListNode cur = head;
		while(cur != null){
			System.out.print(cur.value);
			cur = cur.next;
		}
	}
}
class ListNode{
	public int value;
	public ListNode next;
	
	public ListNode(int value){
		this.value = value;
	}
}

```
