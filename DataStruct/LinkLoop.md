>题目

判断单链表是否有环，一种基于快慢双指针法，一种基于hash存储方法；

- 实现

（1）快指针一次走两步，慢指针一次走一步，如果快指针的值等于慢指针，则有环；

（2）hash存储单链表中的键，遍历中判断是否有值，有则有环；

```
package Chapter2;

import java.util.HashMap;

/**
 * @author Ethan
 * @desc 判断单链表是否有环
 */
public class LinkLoop {
	
	/**
	 * @author Ethan
	 * @desc 基于快慢指针的判断方法
	 */
	public static boolean hasLoop1(Node head){
		Node slow = head;
		Node fast = head.next;
		
		while(fast != null){
			slow = slow.next;
			//此处不能连续走两步，存在null的next节点
			fast = fast.next;
			if(fast == null){
				return false;
			}
			fast = fast.next;
			if(fast == null){
				return false;
			}
			if(slow.value == fast.value){
				return true;
			}
		}
		return false;
	}
	
	/**
	 * @author Ethan
	 * @desc 基于Hash存储的判断方法
	 */
	public static boolean hasLoop2(Node head){
		Node temp = head;
		HashMap<Node,Node> hash = new HashMap<Node,Node>();
		while(temp != null){
			if(hash.get(temp) != null){
				return true;
			}else {
				hash.put(temp, temp);
			}
			temp = temp.next;
			if(temp == null){
				return false;
			}
		}
		return false;
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
		five.next = null;
		
		boolean res = hasLoop2(one);
		System.out.println(res);
	}
}

```
