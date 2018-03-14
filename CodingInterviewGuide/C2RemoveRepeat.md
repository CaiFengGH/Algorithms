>题目

删除无序链表中重复的节点，要求两种方法，一种时间复杂度为O(N)，一种空间复杂度为O(1);

- 实现

（1）方法一：使用HashSet存储链表节点中的值，指针移动到新节点时，判断其中是否包含新节点；

（2）方法二：类似于选择排序，每次遍历删除相同的节点；

```
package Chapter2;

import java.util.HashSet;

/**
 * @author Ethan
 * @desc 删除无序链表中重复的节点
 */
public class C2RemoveRepeat {

	/**
	 * @author Ethan
	 * @desc 时间复杂度为O(N) 
	 * 基于HashSet存储，空间复杂度为O(N)
	 */
	public Node removeRep1(Node head){
		if(head == null){
			return null;
		}
		//初始化HashSet
		HashSet<Integer> set = new HashSet<Integer>();
		set.add(head.value);
		Node pre = head;
		Node curr = head.next;
		
		while(curr != null){
			if(set.contains(curr.value)){
				pre.next = curr.next;
			}else{
				set.add(curr.value);
				pre = curr;
			}
			curr = curr.next;
		}
		return head;
	}
	
	/**
	 * @author Ethan
	 * @desc 空间复杂度为O(1)
	 * 类似于选择排序
	 */
	public Node removeRep2(Node head){
		if(head == null){
			return null;
		}
		//初始化节点
		Node curr = head;
		Node pre = null;
		Node next = null;
		
		while(curr != null){
			pre = curr;
			next = curr.next;
			
			while(next != null){
				if(next.value == curr.value){
					pre.next = next.next;
				}else{
					pre = next;
				}
				next = next.next;
			}
			curr = curr.next;
		}
		return head;
	}
	
	public static void main(String[] args) {
		Node a = new Node(1);
		Node b = new Node(2);
		Node c = new Node(3);
		Node d = new Node(3);
		Node e = new Node(4);
		Node f = new Node(2);
		Node g = new Node(1);
		a.next = b;
		b.next = c;
		c.next = d;
		d.next = e;
		e.next = f;
		f.next = g;
		printList(a);
		System.out.println();
		C2RemoveRepeat removeRepeat = new C2RemoveRepeat();
		Node newHead = removeRepeat.removeRep2(a);
		printList(newHead);
	}
	
	public static void printList(Node head){
		while(head != null){
			System.out.print(head.value);
			head = head.next;
		}
	}
}

```
