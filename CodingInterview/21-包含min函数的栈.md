>题目描述

实现一个包含最小值函数的栈；

- 注意事项

使用数据栈和最小栈(辅助栈)，数据栈中存取数据，最小栈中存取每次最小值；

```

 * @author Ethan
 * @desc 包含最小函数的栈
 */
public class MinStack {
	//输出化数据栈和最小栈
	private MyStack minStack = new MyStack();
	private MyStack dataStack = new MyStack();
	/**
	 * @desc 实现最小栈的压栈操作
	 * @param value
	 */
	public void push(int value){
		dataStack.push(value);
		if(minStack.len == 0 || value < minStack.head.value){
			minStack.push(value);
		}else{
			minStack.push(minStack.head.value);
		}
	}
	/**
	 * @desc 实现最小栈的出栈操作
	 * @return 返回出栈节点
	 */
	public ListNode pop(){
		if(dataStack.len == 0 || minStack.len == 0){
			return null;
		}
		minStack.pop();
		return dataStack.pop();
	}
	/**
	 * @desc 实现最小栈的最小值操作
	 * @return 返回最小节点
	 */
	public ListNode min(){
		if(minStack.len == 0){
			return null;
		}
		ListNode minNode = minStack.head;
		return minNode;
	}
}
/**
 * @author Ethan
 * @desc 基于链表节点生成的栈
 */
class MyStack{
	public ListNode head;
	public int len;
	/**
	 * @desc 链表栈压栈
	 * @param value 压栈值
	 */
	public void push(int value){
		//初始化节点
		ListNode node = new ListNode(value);
		//采用头插法
		node.next = head;
		head = node;
		len++;
	}
	/**
	 * @desc 链表栈出栈
	 * @return 返回出栈值
	 */
	public ListNode pop(){
		if(len == 0){
			return null;
		}else{
			ListNode temp = head;
			head = head.next;
			len--;
			return temp;
		}
	}
	/**
	 * @desc 返回当前栈是否为空
	 * @return true:空
	 */
	public boolean isEmpty(){
		return len == 0;
	}
	/**
	 * @desc 返回当前栈的大小
	 * @return 栈大小
	 */
	public int size(){
		return len;
	}
}
/**
 * @author Ethan
 * @desc 基于链表栈的节点
 */
class ListNode{
	public int value;
	public ListNode next;
	public ListNode(int value){
		this.value = value;
	}
}
```
