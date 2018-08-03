>题目

在有序环形单链表中插入数值，返回新的有序单链表，时间复杂度为O(N)，空间复杂度为O(1);

- 实现

（1）初始化curr和next指针移动来寻找元素位置；

（2）若num值不在有序环形链表的范围内，则如果大于最大值，返回头节点，如果小于最小值，返回此节点；

```
package Chapter2;

/**
 * @author Ethan
 * @desc 在环形单链表中插入整数值，返回新的有序链表的头节点 
 */
public class C2InsertNum {

	public static Node insertNum(Node head,int num){
		Node newNode = new Node(num);
		//1-参数异常
		if(head == null){
			newNode = newNode.next;
			return newNode;
		}
		
		//2-初始化比较节点
		Node curr = head;
		Node next = head.next;
		Node temp = null;
		
		while(next.value >= curr.value){
			if(num <= next.value && num >= curr.value){
				curr.next = newNode;
				newNode.next = next;
				return head;
			}
			temp = next.next;
			curr = next;
			next = temp;
		}
		//3-插入值不在环形单链表范围内
		curr.next = newNode;
		newNode.next = next;
		//4-新增节点最大或者节点最小
		if(num >= curr.value){
			return head;
		}else{
			return newNode;
		}
	}
	
	public static void printList(Node head){
		Node node = head;
		while(node != null){
			System.out.print(node.value+"_");
			node = node.next;
			//环形节点打印一遍即跳出
			if(node == head){
				break;
			}
		}
		System.out.println();
	}
	
	public static void main(String[] args) {
                //构建环形单链表
                Node a = new Node(1);
		Node b = new Node(3);
		Node c = new Node(3);
		Node d = new Node(7);
		Node e = new Node(9);
		a.next = b;
		b.next = c;
		c.next = d;
		d.next = e;
		e.next = a;
		
		//插入前
		printList(a);
		Node newNode = insertNum(a,0);
		//插入后
		printList(newNode);
	}
}
```
