>最大栈

仅使用一个栈实现获取栈最大元素方法；

- 实现方法

在每次压栈操作时，如果当前值大于等于最大值，则先压入当前最大值，更新最大值，再压入当前值；

在每次出栈时，如果出栈元素是当前最大值，则再次出栈，此时出栈元素是当前最大值；

```
package DayCode;

import java.util.Stack;

public class MaxStack {
	
	private int max = Integer.MIN_VALUE;
	private Stack<Integer> stack;
	
	public MaxStack(){
		stack = new Stack<Integer>();
	}
	
	public void push(int x){
		if(x >= max){
			stack.push(max);
			max = x;
		}
		stack.push(x);
	}
	
	public void pop(){
		if(stack.pop() == max) max = stack.pop();
	}
	
	public int top(){
		return stack.peek();
	}
	
	public int getMax(){
		return max;
	}
}
```
