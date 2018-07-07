```
package Chapter2;

/**
 * @author Ethan
 * @desc 单链表的相交问题 
 */
public class C2IntersectNodeInSingleLinkedList {

	/**
	 * @author Ethan
	 * @desc 返回环的入口节点，无环则为空
	 */
	public Node getLoopNode(Node head){
		//1-异常参数检测 构成环至少需要两个节点
		if(head == null || head.next == null || head.next.next == null){
			return null;
		}
		
		//2-初始化快慢指针 
		Node fast = head;
		Node slow = head;
		
		//3-快慢指针移动，快指针一次两步，慢指针一次一步
		while(fast.next != null || fast.next.next != null){
			fast = fast.next.next;
			slow = slow.next;
			if(fast == slow){
				//4-有环，则快指针初始化为head
				fast = head;
				
				//5-快慢指针每次一步前进，直到相遇
				while(fast != slow){
					fast = fast.next;
					slow = slow.next;
				}
				return fast;
			}
		}
		return null;
	}
	
	/**
	 * @author Ethan
	 * @desc 两个无环单链表的重复节点
	 */
	public Node noLoop(Node head1,Node head2){
		//1-异常参数检测，head1和head2检测
		if(head1 == null || head2 == null){
			return null;
		}
		//2-依次计算两个链表的长度 len1和len2
		Node cur1 = head1;
		Node cur2 = head2;
		int len1 = 1;
		int len2 = 1;
		while(cur1.next != null){
			len1++;
			cur1 = cur1.next;
		}
		while(cur2.next != null){
			len2++;
			cur2 = cur2.next;
		}
		int res = len1 - len2;
		
		//3-较长的链表优先移动len1-len2的绝对值步
		cur1 = res > 0 ? head1 : head2;
		cur2 = cur1 == head1 ? head2 : head1;
		
		res = res > 0 ? res : -res;
		
		while(res != 0){
			res--;
			cur1 = cur1.next;
		}
		
		//4-两个链表共同移动，直到相等
		while(cur1 != cur2){
			cur1 = cur1.next;
			cur2 = cur2.next;
		}
		
		return cur1;
	}
	
	
	/**
	 * @author Ethan
	 * @desc 两个单链表均有环，不相交或者相交，相交有loop1与loop2是否相等之说 
	 */
	public Node bothLoop(Node head1,Node loop1,Node head2,Node loop2){
		Node cur1 = null;
		Node cur2 = null;
		if(loop1 == loop2){
			cur1 = head1;
			cur2 = head2;
			int len1 = 1;
			int len2 = 1;
			while(cur1.next != loop1){
				len1++;
				cur1 = cur1.next;
			}
			while(cur2.next != loop2){
				len2++;
				cur2 = cur2.next;
			}
			int res = len1 - len2;
			
			//3-较长的链表优先移动len1-len2的绝对值步
			cur1 = res > 0 ? head1 : head2;
			cur2 = cur1 == head1 ? head2 : head1;
			
			res = res > 0 ? res : -res;
			
			while(res != 0){
				res--;
				cur1 = cur1.next;
			}
			//4-两个链表共同移动，直到相等
			while(cur1 != cur2){
				cur1 = cur1.next;
				cur2 = cur2.next;
			}
			return cur1;
		}else{
			//是否两个环并到一起
			cur1 = loop1;
			while(cur1.next != loop1){
				if(cur1 == loop2){
					return loop1;
				}
				cur1 = cur1.next;
			}
			return null;
		}
	}
	
	/**
	 * @author Ethan
	 * @desc 用来获取单链表的相交节点 
	 */
	public Node getIntersectNode(Node head1,Node head2){
		//1-异常参数检测
		if(head1 == null || head2 == null){
			return null;
		}
		//2-获取两个单链表的环入口节点
		Node loop1 = getLoopNode(head1);
		Node loop2 = getLoopNode(head2);
		
		//3-均无环情况
		if(loop1 == null && loop2 == null){
			noLoop(head1,head2);
		}
		
		//4-均有环情况
		if(loop1 != null && loop2 != null){
			bothLoop(head1,loop1,head2,loop2);
		}
		
		//5-一个有环一个无环不相交
		return null;
	}
	
	
	/**
	 * @author Ethan
	 * @desc 用于验证各个基本方法是否正确
	 */
	public static void main(String[] args) {
		C2IntersectNodeInSingleLinkedList c2 = 
				new C2IntersectNodeInSingleLinkedList(); 

		Node a = new Node(1);
		Node b = new Node(2);
		Node c = new Node(3);
		Node d = new Node(4);
		Node e = new Node(5);
		Node f = new Node(6);
		
		a.next = b;
		b.next = c;
		c.next = d;
		d.next = e;

		f.next = d;
		
		Node res = c2.bothLoop(a,d,f,d);
		
		if(res != null){
			System.out.println(res.value);
		}
	}
}
```
