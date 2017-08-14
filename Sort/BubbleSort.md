>冒泡排序

- 工作原理

从前向后进行遍历，比较相邻两个数，若前者大于后者，则交换位置，一次遍历，最大数位于最尾部；
依次进行遍历，直至所有数字有序排列；

- 注意事项

若一次遍历中，未发生交换，则已经实现有序排列；
冒泡排序的时间复杂度为O(n2);

```
public class BubbleSort {
	
	private int i = 0;
	private int j = 0;
	private int temp = 0;
	
	/**
	 * @desc 无标记的冒泡排序
	 * @param arr 数组
	 * @param len 数组长度
	 * @return int[] 数组
	 */
	public void bubbleSort1(int[] arr,int len){
		//外循环表示遍历次数
		for(i = len - 1; i > 0; i--){
			//内循环表示比较交换操作
			for(j = 0; j < i; j++){
				if(arr[j] > arr[j+1]){
					temp = arr[j];
					arr[j] = arr[j+1];
					arr[j+1] = temp;
				}
			}
		}
	}
	
	
	/**
	 * @desc 有标记的冒泡排序
	 * @param arr 数组
	 * @param len 数组长度
	 * @return int[] 数组
	 */
	public void bubbleSort2(int[] arr,int len){
		//flag表示是有一次遍历中有交换，0:没有  1:有
		int flag = 0;
		//外循环表示遍历次数
		for(i = len - 1; i > 0; i--){
			//内循环表示比较交换操作
			for(j = 0; j < i;j++){
				if(arr[j] > arr[j+1]){
					temp = arr[j];
					arr[j] = arr[j+1];
					arr[j+1] = temp;
					
					flag = 1;
				}
			}
			//判断一次遍历无交换则跳出
			if(flag == 0){
				break;
			}
		}
	}
}
```

[图片详解](http://images.cnitblog.com/i/497634/201403/121521153545888.jpg)
