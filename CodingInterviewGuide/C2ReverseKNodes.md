```
package Chapter2;

import java.util.Stack;

/**
 * @author Ethan
 * @desc 每隔k个节点逆序 
 */
public class C2ReverseKNodes {
	
	/**
	 * @author Ethan
	 * @desc 每隔k个节点逆序
	 * 1->2->3->4->5->6 k:2 2->1->4->3->6->5
	 * 1->2->3->4->5 k:2 2->1->4->3->5
	 */
	public Node reverseKNodes(Node head,int k){
		//1-异常参数检测
		if(head == null || k < 2){
			return head;
		}
		//2-初始化 pre: next: cur: newHead:
		Node pre = null; 
		Node next = null; 
		Node cur = head; 
		Node newHead = head; 
		
		//3-初始化栈
		Stack<Node> stack = new Stack<Node>();
		
		//4-遍历逆序
		while(cur != null){
			next = cur.next;
			stack.push(cur);
			if(stack.size() == k){
				pre = reverse(stack,pre,next);
				newHead = newHead == head ? cur : newHead;
			}
			cur = next;
		}
		return newHead;
	}

	/**
	 * @author Ethan
	 * @desc k节点逆序 
	 */
	private Node reverse(Stack<Node> stack, Node left, Node right) {
		//1-当前组的第一个节点被前一个组的最后一个节点连接
		Node next = null;
		Node cur = stack.pop();
		if(left != null){
			left.next = cur;
		}
		//2-k节点间逆序
		while(!stack.isEmpty()){
			next = stack.pop();
			cur.next = next;
			cur = next;
		}
		
		//3-当前组的最后一个节点连接下一个组的第一个节点
		cur.next = right;
		return cur;
	}
	
	/**
	 * @author Ethan
	 * @desc 打印单链表 
	 */
	public void printList(Node head){
		Node cur = head;
		while(cur != null){
			System.out.print(cur.value + "->");
			cur = cur.next;
		}
		System.out.println();
	}
	
	/**
	 * @author Ethan
	 * @desc 
	 * 1->2->3->4->5 k:2 2->1->4->3->5
	 */
	public static void main(String[] args) {
		
		C2ReverseKNodes rk = new C2ReverseKNodes();
		
		Node a = new Node(1);
		Node b = new Node(2);
		Node c = new Node(3);
		Node d = new Node(4);
		Node e = new Node(5);
		
		a.next = b;
		b.next = c;
		c.next = d;
		d.next = e;
		
		rk.printList(a);
		
		Node res = rk.reverseKNodes(a, 2);

		rk.printList(res);
	}
}
```
