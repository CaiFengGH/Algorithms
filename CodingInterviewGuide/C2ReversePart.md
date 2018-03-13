>题目

反转部分单链表，传递参数head/from/to，

- 实现

（1）from/to的异常参数检测；

（2）反转的部分是否包含头部；

（3）反转部分中节点的移动情况；

```
package Chapter2;

/**
 * @author Ethan
 * @desc 实现单链表部分反转
 */
public class C2ReversePart {
	
	/**
	 * @author Ethan
	 * @desc 
	 */
	public Node reversePart(Node head,int from,int to){
		int len = 0;
		Node fPre = null;
		Node tPos = null;
		Node node = head;
		//计算单链表长度，且初始化fPre和tPos
		while(node != null){
			len++;
			if(len == from - 1){
				fPre = node;
			}
			if(len == to + 1){
				tPos = node;
			}
			node = node.next;
		}
		//进行form和to的异常参数检测
		if(from > to || from < 1 || to > len){
			return head;
		}
		//确定反转头
		node = fPre == null ? head : fPre.next;
		//开始进行反转操作
		Node node1 = node.next;
		node.next = tPos;
		Node next = null;
		
		while(node1 != tPos){
			next = node1.next;
			node1.next = node;
			node = node1;
			node1 = next;
		}
		//是否从头开始反转
		if(fPre != null){
			fPre.next = node;
			return head;
		}
		return node;
	}
	
	public static void main(String[] args) {
		Node one = new Node(1);
		Node two = new Node(2);
		Node three = new Node(3);
		Node four = new Node(4);
		Node five = new Node(5);
		one.next = two;
		two.next = three;
		three.next = four;
		four.next = five;
		
		printLinkedList(one);
		//反转部分链表
		C2ReversePart reverse = new C2ReversePart();
		Node resHead = reverse.reversePart(one, 1, 6);
		//循环打印链表
		printLinkedList(resHead);
	}

	private static void printLinkedList(Node head) {
		while(head != null){
			System.out.println(head.value);
			head = head.next;
		}
	}
}
```
