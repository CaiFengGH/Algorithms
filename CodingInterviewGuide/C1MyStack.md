>题目

实现一个具有getMin功能的栈；

```
package Chapter1;

import java.util.Stack;

/**
 * @author Ethan
 * @desc 实现一个具有getMin功能的栈
 */
public class C1MyStack {

	//stackData:存储数据 stackMin:存储最小值
	private Stack<Integer> stackData;
	private Stack<Integer> stackMin;
	
	public C1MyStack(){
		stackData  = new Stack<Integer>();
		stackMin = new Stack<Integer>();
	}
	
	//实现压入规则：压入stackData,若元素小于stackMin栈顶元素，则压入，否则再次压入栈顶元素
	public void push(int num){
		if(stackMin.isEmpty()){
			stackMin.push(num);
		}else if(num < this.getMin()){
			stackMin.push(num);
		}else{
			int temp = stackMin.peek();
			stackMin.push(temp);
		}
		stackData.push(num);
	}
	
	//实现弹出规则：弹出stackData,同时弹出stackMin栈顶元素
	public int pop(){
		if(stackData.isEmpty()){
			throw new RuntimeException();
		}
		stackMin.pop();
		return stackData.pop();
	}
	
	//实现获取最小值
	public int getMin(){
		return stackMin.peek();
	}
}
```
