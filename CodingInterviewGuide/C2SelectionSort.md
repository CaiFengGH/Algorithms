```
package Chapter2;

/**
 * @author Ethan
 * @desc 单链表的选择排序 
 */
public class C2SelectionSort {

	/**
	 * @author Ethan
	 * @desc 在单链表中实现排序 
	 */
	public Node selectionSort(Node head){
		//1-初始化 small:最小 smallPre:最小的前一个 tail:已排序的尾部 cur:未排序首部
		Node smallPre = null;
		Node small = null;
		Node tail = null;
		Node cur = head; 
		
		//2-选择排序
		while(cur != null){
			small = cur;
			smallPre = getSmallPre(small);
			if(smallPre != null){
				small = smallPre.next;
				smallPre.next = smallPre.next.next;
			}
			cur = cur == small ? cur.next : cur;
			if(tail == null){
				head = small;
			}else{
				tail.next = small;
			}
			tail = small;
		}
		return head;
	}

	/**
	 * @author Ethan
	 * @desc 返回未排序链表中的最小节点 
	 */
	private Node getSmallPre(Node head) {
		//1-初始化 small smallPre pre cur
		Node smallPre = null;
		Node small = head;
		Node pre = head;
		Node cur = head.next; 
		
		//2-遍历查找
		while(cur != null){
			if(cur.value < small.value){
				smallPre = pre;
				small = cur;
			}
			pre = cur;
			cur = cur.next;
		}
		return smallPre;
	}
	
	public void printList(Node head){
		Node cur = head;
		while(cur != null){
			System.out.print(cur.value + "->");
			cur = cur.next;
		}
		System.out.println();
	}
	
	public static void main(String[] args) {
		Node a = new Node(1);
		Node b = new Node(5);
		Node c = new Node(3);
		Node d = new Node(4);
		Node e = new Node(2);
		
		a.next = b;
		b.next = c;
		c.next = d;
		d.next = e;
		
		C2SelectionSort ss = new C2SelectionSort();
		ss.printList(a);
		
		Node head = ss.selectionSort(a);
		ss.printList(head);
	}
}
```
