>选择排序

- 排序原理

在未排序数列中，选择最小或者最大值置于首部；

再未排序数列中继续选择最小值或最大值置于已排序数列的尾部；

- 注意事项

选择排序的时间复杂度为O(N*N)

```
/**
 * @author Ethan
 * @desc 实现选择排序
 * @date 2017年8月14日
 */
public class SelectionSort {
	
	/**
	 * @desc 选择排序
	 * @param arr 数组
	 */
	public void selectionSort(int[] arr){
		//min记录每次遍历时的最小值索引
		int minIndex = 0;
		int len = arr.length;
		int i = 0;
		int j = 0;
		
		for(i = 0; i < len; i++ ){
			//初始化最小值
			minIndex = i;
			for(j = i + 1; j < len; j++){
				//记录每次遍历最小值下标
				if(arr[j] < arr[minIndex]){
					minIndex = j;
				}
			}
			//将最小值与初始化最小值替换
			if(minIndex != i){
				int temp = arr[minIndex];
				arr[minIndex] = arr[i];
				arr[i] = temp;
			}
		}
	}
}
```

[图片详解](http://images.cnitblog.com/i/497634/201403/130003333397123.jpg)
