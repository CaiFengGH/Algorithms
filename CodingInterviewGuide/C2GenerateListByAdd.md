```
package Chapter2;

import java.util.Stack;

/**
 * @author Ethan
 * @desc 将两个单链表表示的整数相加，基于单链表表示 
 */
public class C2GenerateListByAdd {

	/**
	 * @author Ethan
	 * @desc 基于栈实现低位相加
	 */
	public Node addList(Node head1,Node head2){
		//1-异常参数判断
		if(head1 == null){
			return head2 == null ? null : head2;
		}else{
			if(head2 == null){
				return head1;
			}
		}
		
		//2-初始化栈
		Stack<Integer> stack1 = new Stack<Integer>();
		Stack<Integer> stack2 = new Stack<Integer>();
		
		while(head1 != null){
			stack1.push(head1.value);
			head1 = head1.next;
		}
		while(head2 != null){
			stack2.push(head2.value);
			head2 = head2.next;
		}
		
		//3-初始化 add1:加数1 add2:加数2 carry:进位 pre:前一个节点
		int add1 = 0;
		int add2 = 0;
		int carry = 0;
		int sum = 0;
		
		Node pre = null; 
		Node node = null; 
		
		//4-实现加法
		while(!stack1.isEmpty() || !stack2.isEmpty()){
			add1 = stack1.isEmpty() ? 0 : stack1.pop();
			add2 = stack2.isEmpty() ? 0 : stack2.pop();
			sum = add1 + add2 + carry;
			
			pre = node;
			node = new Node(sum % 10);
			node.next = pre;
			carry = sum / 10;
		}
		
		//5-判断是否存在进位
		if(carry == 1){
			pre = node;
			node = new Node(1);
			node.next = pre;
		}
		
		return node;
	}
}
```
