>题目

删除单链表中值为value的节点，返回新链表的头节点；

- 实现

（1）值为value节点的位置，头节点和非头节点；

（2）值为value节点的数量，一个或者多个，连续或者不连续；

```
/**
 * @author Ethan
 * @desc 移除单链表中值为value的节点 
 */
public class C3RemoveValue {

	public Node removeValue(Node head,int value){
		//头部寻找到第一个非value值节点
		while(head != null){
			if(head.value != value){
				break;
			}
			head = head.next;
		}
		
		//删除单链表中值为value的节点
		Node curr = head;
		Node pre = head;
		while(curr != null){
			//如果当前节点与value相同
			if(curr.value == value){
				pre.next = curr.next;
			}else{
				pre = curr;
			}
			curr = curr.next;
		}
		return head;
	}
}
```
