>题目

使用两个栈实现一个队列，实现add/pop/peek方法；

- 注意

（1）一次入栈和出栈操作，则12345从54321变为12345；

（2）stackPush:入栈 stackPop:出栈 当两者均为空时，抛出异常；当后者为空时，将前者全部出栈压入后者；
    后者不为空为，add直接在stackPush中压栈，peek直接返回stackPop.peek()元素；
    

```
import java.util.Stack;

/**
 * @author Ethan
 * @desc 基于两个栈实现队列 
 */
public class C2TwoStacksQueue {

	//初始化栈
	private Stack<Integer> stackPush;
	private Stack<Integer> stackPop;
	
	public C2TwoStacksQueue(){
		stackPush = new Stack<Integer>();
		stackPop = new Stack<Integer>();
	}
	
	//队列入队:add
	public void add(int value){
		stackPush.push(value);
	}
	
	//队列出队:pop
	public int pop(){
		if(stackPush.isEmpty() && stackPop.isEmpty()){
			throw new RuntimeException("队列无元素，无法出队");
		}else if(stackPop.isEmpty()){
			push2Pop();
		}
		return stackPop.pop();
	}

	//队列首位元素:peek
	public int peek(){
		if(stackPush.isEmpty() && stackPop.isEmpty()){
			throw new RuntimeException("队列无元素，无队首元素");
		}else if(stackPop.isEmpty()){
			push2Pop();
		}
		return stackPop.peek();
	}
	
	//从stackPush到stackPop操作:push2Pop
	private void push2Pop() {
		while(!stackPush.isEmpty()){
			stackPop.push(stackPush.pop());
		}
	}
}

```
