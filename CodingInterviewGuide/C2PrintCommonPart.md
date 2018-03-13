>题目

给定两个有序链表的头节点，打印出其公共部分；

- 实现

（1）通过移动链表寻找公共节点；

（2）直到某个链表的next指针指向null；

```
/**
 * @author Ethan
 * @desc 打印两个有序链表的公共部分
 */
public class C2PrintCommonPart {
	
	public void printCommonPart(Node head1,Node head2){
		System.out.println("Common part:");
		while(head1 != null && head2 != null){
			//寻找第一个公共节点
			if(head1.value < head2.value){
				head1 = head1.next;
			}else if(head1.value > head2.value){
				head2 = head2.next;
			}else {
				System.out.println(head1.value);
				head1 = head1.next;
				head2 = head2.next;
			}
		}
		System.out.println();
	}
}
class Node{
	public int value;
	public Node next;
}
```
