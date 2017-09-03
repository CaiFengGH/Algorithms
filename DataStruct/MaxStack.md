>最大栈

保存栈中最大元素的栈；

- 实现方法

在插入栈顶元素时，直接保存最大元素索引值，返回最大元素时间复杂度为O(1)；

```
/**
 * @author Ethan
 * @desc
 */
public class MaxStack {
	//存储元素的数组，栈顶元素，保存当前最大元素的索引，保存最大元素索引的数组，数据项
	private int[] stackItem;
	private int stackTop = -1;
	private int maxStackItemIndex;
	private int[] nextMaxStackItem;
	private int numItem;
	
	public MaxStack(int numItem){
		this.numItem = numItem;
		stackItem = new int[numItem];
		nextMaxStackItem = new int[numItem];
		maxStackItemIndex = -1;
	}
	/**
	 * @desc 压栈
	 */
	public void push(int data){
		if(stackTop == numItem - 1){
			System.out.println("栈已满，不能添加");
			return ;
		}
		//添加元素
		stackTop++;
		stackItem[stackTop] = data;
		//在栈顶确定最大值索引
		if(data > max()){
			nextMaxStackItem[stackTop] = maxStackItemIndex;
			//更新之前最大值索引
			maxStackItemIndex = stackTop;
		}else{
			nextMaxStackItem[stackTop] = -1;
		}
	}
	/**
	 * @desc 出栈 
	 */
	public int pop(){
		//异常检测
		if(stackTop == -1){
			System.out.println("栈已空，不能再出栈");
		}
		int res = stackItem[stackTop];
		//更新最大值索引
		if(stackTop == maxStackItemIndex){
			maxStackItemIndex = nextMaxStackItem[stackTop];
		}
		stackTop--;
		return res;
	}
	/**
	 * @desc 返回栈中最大值元素 
	 */
	public int max(){
		if(maxStackItemIndex >= 0){
			return stackItem[maxStackItemIndex];
		}else{
			return -1;
		}
	}
	/**
	 * @desc 测试最大栈 
	 */
	public static void main(String[] args) {
		MaxStack ms = new MaxStack(5);
		ms.push(1);
		ms.push(3);
		ms.push(4);
		ms.push(2);
		System.out.println(ms.max());
		ms.pop();
		System.out.println(ms.max());
	}
}
```
