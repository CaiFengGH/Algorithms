>最大堆

每一个节点的值，均大于其子节点的值，类似于完整二叉树结构；

- 实现方法

借助ArrayList实现最大堆；

```
import java.util.ArrayList;
import java.util.List;

/**
 * @author Ethan
 * @desc 最大堆
 */
public class MaxHeap<T extends Comparable<T>> {
	//存放堆的动态数组
	private List<T> maxHeap;
	
	public MaxHeap(){
		this.maxHeap = new ArrayList<T>();
	}
	
	/**
	 * @desc 添加元素
	 * @param data 元素
	 */
	public void insert(T data){
		//将元素添加到数组末尾
		maxHeap.add(data);
		int size = maxHeap.size();
		//将末尾元素进行向上移动
		fillUp(size - 1);
	}
	/**
	 * @desc 向上填充
	 * @param start 填充开始位置，通常为末尾
	 */
	private void fillUp(int start) {
		//初始化当前索引和父节点索引
		int current = start;
		int parent = (current - 1) / 2;
		T temp = maxHeap.get(start);
		//循环向上移动元素
		while(current > 0){
			//当前元素与父节点元素比较
			int compare = maxHeap.get(parent).compareTo(temp);
			//父节点大，则跳出；父节点小，则继续
			if(compare >= 0){
				break;
			}else{
				//将父节点元素移动到当前索引位置
				maxHeap.set(current, maxHeap.get(parent));
				current = parent;
				parent = (current - 1) / 2;
			}
		}
		//在合适位置设置当前节点
		maxHeap.set(current, temp);
	}
	
	/**
	 * @desc 删除元素
	 * @param data 元素值
	 * @return -1：未删除 0：删除
	 */
	public int remove(T data){
		//异常输入之堆为空
		if(maxHeap.isEmpty()){
			System.out.println("堆为空不能删除");
			return -1;
		}
		//异常输入之不存在元素
		if(maxHeap.indexOf(data) == -1){
			System.out.println("该元素不存在，不能删除");
			return -1;
		}
		//寻找元素所在位置
		int index = maxHeap.indexOf(data);
		//将末尾元素置于删除位置
		int oldSize = maxHeap.size();
		maxHeap.set(index, maxHeap.get(oldSize - 1));
		maxHeap.remove(oldSize - 1); 
		//向下移动，保证堆的二叉树性质
		int newSize = maxHeap.size();
		if(newSize > 1){
			fillDown(index,newSize - 1);
		}
		return 0;
	}
	/**
	 * @desc 向下填充
	 * @param index 开始索引
	 * @param end 结束索引，通常为堆尾部
	 */
	private void fillDown(int index, int end) {
		//初始化当前索引和左子节点索引
		int current = index;
		int leftChild = 2 * index + 1;
		T temp = maxHeap.get(index);
		//开始循环向下移动
		while(leftChild < end){
			//比较左子节点和右子节点的大小
			int compare = maxHeap.get(leftChild).compareTo(maxHeap.get(leftChild + 1));
			if(compare < 0){
				leftChild++;
			}
			//当前节点和子节点中较大者比较，大则跳出，小则移动
			if(maxHeap.get(leftChild).compareTo(temp) < 0 ){
				break;
			}else{
				//在当前索引处设置元素，更改当前索引和左子节点索引值
				maxHeap.set(current, maxHeap.get(leftChild));
				current = leftChild;
				leftChild = 2 * current + 1; 
			}
		}
		//在当前索引处设置值
		maxHeap.set(current, temp);
	}

	@Override
	public String toString() {
		StringBuilder sb = new StringBuilder();
		int size = maxHeap.size();
		for(int i = 0; i < size; i++){
			sb.append(maxHeap.get(i)+" ");
		}
		return sb.toString();
	}
	
	public static void main(String[] args) {
		int[] arr = {10,20,30,40,50,60,70,80,90};
		MaxHeap<Integer> maxHeap = new MaxHeap<Integer>();
		for(int i = 0; i < arr.length; i++){
			maxHeap.insert(arr[i]);
		}
		/*
		 *        90
		 *       /  \
		 *     80    60
		 *     / \  / \  
		 *   70  3020  50
		 *   / \
		 *  10 40
		 * */
		System.out.println("最大堆为："+maxHeap);
		maxHeap.insert(100);

		/*        100
		 *       /   \
		 *      90    60
		 *     /  \   / \  
		 *   70   80 20  50
		 *   / \  /
		 *  10 40 30
		 * */
		System.out.println("添加100最大堆为："+maxHeap);
		maxHeap.remove(10);
		/*        100
		 *       /   \
		 *      90    60
		 *     /  \   / \  
		 *   70   80 20  50
		 *   / \  
		 *  30 40 
		 * */
		System.out.println("删除10最大堆为："+maxHeap);
	}
}
```

[图示添加](http://images.cnitblog.com/i/497634/201403/182345301461858.jpg)

[图示删除](http://images.cnitblog.com/i/497634/201403/182348387716132.jpg)
