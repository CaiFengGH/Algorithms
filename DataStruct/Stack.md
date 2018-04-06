>栈

- 基于数组实现栈

```
/**
 * @author Ethan
 * @desc 基于数组实现的栈
 * @date 2017年8月16日
 */
public class ArrayStack {
	private int[] arr;
	private int top = -1;
	
	public ArrayStack(int size){
		arr = new int[size];
	}
	
	/**
	 * @desc 压栈
	 * @param value
	 * @return 是否压栈成功
	 */
	public boolean push(int value){
		arr[++top] = value;
		return true;
	}
	
	/**
	 * @desc 出栈
	 * @return 是否出栈成功
	 */
	public int pop(){
		if(isEmpty()){
			return -1;
		}
		int temp = arr[top--];
		return temp;
	}
	
	/**
	 * @desc 栈顶元素
	 * @return 返回栈顶元素
	 */
	public int peek(){
		if(isEmpty()){
			return -1;
		}
		return arr[top];
	}
	
	/**
	 * @desc 是否为空
	 * @return 
	 */
	public boolean isEmpty(){
		return top == -1;
	}

	/**
	 * @desc 打印栈元素
	 */
	public void printStack(){
		if(isEmpty()){
			System.out.println("栈为空");
			return;
		}
		int tmp = top;
		while(tmp >= 0){
			System.out.println(arr[tmp--]);
		}
	}
}
```
