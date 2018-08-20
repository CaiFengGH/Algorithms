```
package Chapter2;

import java.util.Stack;

/**
 * @author Ethan
 * @desc 判断链表是否是回文结构 
 */
public class C2ListIsPalindrome {
	
	/**
	 * @author Ethan
	 * @desc 回文结构 链表压栈后出栈顺序与链表遍历顺序相同 
	 * 偶数 1-2-2-1 出栈顺序1-2-2-1
	 * 奇数 1-2-3-2-1 出栈顺序 1-2-3-2-1
	 */
	public boolean isPalindrome1(Node head){
		//1-异常参数检测
		if(head == null){
			return false;
		}
		//2-初始化栈 stack
		Node cur = head;
		Stack<Node> stack = new Stack<Node>();
		while(cur != null){
			stack.push(cur);
			cur = cur.next;
		}
		
		//3-出栈和遍历比较
		cur = head;
		while(!stack.isEmpty()){
			if(cur.value != stack.pop().value){
				return false;
			}
			cur = cur.next;
		}
		//4-返回结果
		return true;
	}
	
	/**
	 * @author Ethan
	 * @desc 链表右半区入栈后出栈顺序与左半区遍历结果一致
	 * 偶：1-2-2-1 右半区：2-1 左半区：1-2 右半区出栈 1-2 
	 * 奇：1-2-3-2-1 右半区：2-1 左半区：1-2 右半区出栈 1-2
	 */
	public boolean isPalindrome2(Node head){
		//1-异常参数检测
		if(head == null){
			return false;
		}
		//2-确定左右半区分界 无需计算链表长度 
		Node right = head.next;
		Node cur = head;
		while(cur.next != null && cur.next.next != null){
			//一次一步
			right = right.next;
			//一次两步
			cur = cur.next.next;
		}
		
		//3-右半区入栈
		Stack<Node> stack = new Stack<Node>();
		while(right != null){
			stack.push(right);
			right = right.next;
		}
		
		//4-右半区出栈与左半区遍历结果
		cur = head;
		while(!stack.isEmpty()){
			if(cur.value != stack.pop().value){
				return false;
			}
			cur = cur.next;
		}
		//5-返回结果
		return true;
	}
	
	/**
	 * @author Ethan
	 * @desc 时间复杂度为O(N)，空间复杂度为O(1) 
	 */
	public boolean isPalindrome3(Node head){
		//1-异常参数检测
		//2-将链表分为左右半区
		//3-将右半区反转
		//4-从左右半区节点开始遍历
		//5-将右半区再次反转
		return false;
	}
}
```
