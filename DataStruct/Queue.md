>队列

- 基于数组实现队列

```
/**
 * @author Ethan
 * @desc 基于数组实现的队列
 * @date 2017年8月16日
 */
public class ArrayQueue {
	private int MAX;
	private int[] arr;
	private int front;
	private int rear = -1;
	//队列元素个数
	private int numItems;

	public ArrayQueue(int num){
		this.MAX = num;
		arr = new int[num];
	}
	/**
	 * @desc 入队
	 * @param value
	 */
	public void insert(int value){
		arr[++rear] = value;
		if(rear == MAX - 1){
			rear = -1;
		}
		numItems++;
	}
	/**
	 * @desc 出队
	 * @return 返回出队值
	 */
	public int remove(){
		int temp = arr[front++];
		if(front == MAX){
			front =  0;
		}
		numItems--;
		return temp;
	}
	/**
	 * @desc 队首元素
	 * @return 返回队首元素值
	 */
	public int peek(){
		return arr[front];
	}

	/**
	 * @desc 是否为空队列
	 * @return 
	 */
	public boolean isEmpty(){
		return numItems == 0;
	}
	
	/**
	 * @desc 返回队列元素个数
	 * @return
	 */
	public int items(){
		return numItems;
	}
}
```
