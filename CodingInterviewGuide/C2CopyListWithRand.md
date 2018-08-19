```
package Chapter2;

import java.util.HashMap;

/**
 * @author Ethan
 * @desc 复杂链表的复制 
 */
public class C2CopyListWithRand {

	/**
	 * @author Ethan
	 * @desc 基于hashmap的深复制 
	 * 时间复杂度为o(n*n)，空间复杂度为o(n*n)
	 */
	public NodeWithRand copyListWithRand1(NodeWithRand head){
		//1-异常参数检测
		if(head == null){
			return null;
		}
		//2-初始化hashmap
		HashMap<NodeWithRand,NodeWithRand> map = 
				new HashMap<NodeWithRand, NodeWithRand>();
		
		//3-初始化链表节点
		NodeWithRand cur = head; 
		while(cur != null){
			map.put(cur, new NodeWithRand(cur.value));
			cur = cur.next;
		}
		cur = head;
		
		//4-实现next和rand指针的拷贝
		while(cur != null){
			//实现next指针的复制
			map.get(cur).next = map.get(cur.next);
			//实现rand指针的复制
			map.get(cur).rand = map.get(cur.rand);
			
			cur = cur.next;
		}
		
		return map.get(head);
	}
	
	/**
	 * @author Ethan
	 * @desc 基于特殊思路实现复杂链表的复制
	 */
	public NodeWithRand copyListWithRand2(NodeWithRand head){
		//1-异常参数检测
		if(head == null){
			return null;
		}
		
		//2-初始化复制节点，并与原链表穿插
		NodeWithRand cur = head; 
		NodeWithRand next = null;
		
		while(cur != null){
			next = cur.next;
			cur.next = new NodeWithRand(cur.value);
			cur.next.next = next;
			cur = next;
		}
		
		//3-实现复制接点的随机指针
		NodeWithRand copyNode = null; 
		cur = head;
		
		while(cur != null){
			next = cur.next.next;
			copyNode = cur.next;
			copyNode.rand = cur.rand != null ? cur.rand.next : null;
			cur = next;
		}
		
		//4-将原链表与新生成的链表拆开
		cur = head;
		NodeWithRand res = cur.next;

		while(cur != null){
			next = cur.next.next;
			copyNode = cur.next;

			cur.next = next;
			copyNode.next = next != null ? next.next : null;
			
			cur = next;
		}
		//5-返回新的头节点
		return res;
	}
}
 
```
