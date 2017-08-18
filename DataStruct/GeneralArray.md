>普通数组

- 数组方法

实现普通数组的增加、删除、查找和打印功能；
 
- 注意事项

数组增加的时间复杂度O(1)，删除的时间复杂度为O(N),线性搜索的时间复杂度为O(N);

```
/**
 * @author Ethan
 * @desc 实现普通数组的增加、删除、查找和遍历打印
 */
public class GeneralArray {
	/*
	 * size:大小 numItems:元素个数
	 * */
	private int[] arr;
	private int size;
	private int numItems;
	
	public GeneralArray(int max){
		arr = new int[max];
		this.size = max;
		this.numItems = 0;
	}
	/**
	 * @desc 数组添加
	 * @param value 添加值
	 * @return 返回是否添加成功
	 */
	public boolean insert(int value){
		if(numItems == size){
			System.out.println("数组已满，不能再继续添加");
			return false;
		}
		arr[numItems++] = value;
		return true;
	}
	/**
	 * @desc 数组删除 
	 * @param value 删除值
	 * @return 返回是否已经删除
	 */
	public boolean delete(int value){
		//找到value值在数组中的位置
		int i = 0;
		for(i = 0; i < numItems; i++){
			if(arr[i] == value){
				break;
			}
		}
		//判断i值的异常情况
		if(i == numItems){
			System.out.println("该值不存在于数组中");
			return false;
		}
		//考虑数组满时的溢出情况
		if(numItems == size){
			//将数组进行移位操作
			//如果value位于最后一个元素，等价于不删除
			for(int j = i; j < numItems - 1; j++){
				arr[j] = arr[j+1];
			}			
		}else{
			for(int j = i; j < numItems; j++){
				arr[j] = arr[j+1];
			}			
		}
		numItems--;
		return true;
	}
	/**
	 * @desc 查找数组中是否包含此元素 
	 * @param value 目标值
	 * @return 返回是否包含
	 */
	public boolean search(int value){
		int i = 0;
		for(i = 0; i < numItems; i++){
			if(arr[i] == value){
				break;
			}
		}
		if(i == numItems){
			return false;
		}else{
			return true;
		}
	}
	/**
	 * @desc 打印数组
	 */
	public void display(){
		System.out.println("数组如下所示：");
		for(int i = 0; i < numItems; i++){
			System.out.print(arr[i]+" ");
		}
	}
}
```
