```
package Chapter2;

/**
 * @author Ethan
 * @desc 单链表按照左右半区的方式进行重组 
 * 1->2->3 : 1->2->3
 * 1->2->3->4->5->6 : 1->4->2->5->3->6
 */
public class C2RelocateWithLeftAndRight {

	/**
	 * @author Ethan
	 * @desc 按照左右半区的方式进行查找 
	 */
	public void relocate(Node head){
		//1-异常参数检测
		if(head == null || head.next == null){
			return ;
		}
		
		//2-初始化mid节点和right节点
		//mid:链表的中间节点 right:右半区的左边节点
		Node mid = head;
		Node right = head.next;
		
		//快慢指针确定mid和right节点
		while(right.next != null && right.next.next != null){
			mid = mid.next;
			right = right.next.next;
		}
		
		//4-将左右半区链表进行融合
		right = mid.next;
		mid.next = null;
		merge(head,right);
	}

	/**
	 * @author Ethan
	 * @desc 给定两个单链表的头节点，进行融合 
	 * 1->2->3 : 4->5->6  1->4->2->5->3->6
	 */
	private void merge(Node left, Node right) {
		//1-初始化next节点
		Node next = null;
		//2-循环遍历链表赋值
		while(left.next != null){
			next = right.next;
			right.next = left.next;
			left.next = right;
			left = right.next;
			right = next;
		}
		//3-最后left
		left.next = right;
	}
	
	public void printList(Node head){
		Node cur = head;
		while(cur != null){
			System.out.print(cur.value+"->");
			cur = cur.next;
		}
		System.out.println();
	}
	
	public static void main(String[] args) {
		C2RelocateWithLeftAndRight relocate = new 
				C2RelocateWithLeftAndRight();
		
		Node a = new Node(1);
		Node b = new Node(2);
		Node c = new Node(3);
		Node d = new Node(4);
		a.next = b;
		b.next = c;
		c.next = d;
		
		relocate.printList(a);
		
		relocate.relocate(a);
		
		relocate.printList(a);
	}
	
}
```
