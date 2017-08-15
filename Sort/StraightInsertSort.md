>直接插入排序法

- 排序原理

将待排序数组分为无序区与有序区，初始时有序区仅有一个元素，无序区有n-1个元素；

每次从无序区中选取第一个元素，在有序区中选择合适位置插入，使之有序，重复n-1次实现排序；

- 注意事项

直接插入排序的时间复杂度为O(N*N);

```
/**
 * @author Ethan
 * @desc 直接插入排序法
 * @date 2017年8月15日
 */
public class StraightInsertSort {
	/**
	 * @desc 有序区和无序区实现直接插入排序
	 * @param arr 数组
	 * @param len 数组长度
	 */
	public void straightInsertSort(int[] arr,int len){
		//i:从无序区取值 j:寻找小于无序区选择的值索引 k:有序区数组移动
		int i = 0;
		int j = 0;
		int k = 0;
		//从无序区取值
		for(i = 1; i < len; i++){
			//从有序区寻找首个小于所取值的元素下标
			for(j = i - 1; j >= 0; j--){
				if(arr[j] < arr[i]){
					break;
				}
			}
			//将无序区中所取值插入到有序区中
			if(j != i - 1){
				//记录无序区所取值
				int temp = arr[i];
				//通过数组移位，实现插入
				for(k = i - 1; k > j; k--){
					arr[k+1] = arr[k];
				}
				//将所取值插入到指定位置，此时k=j
				arr[j+1] = temp;
			}
		}
	} 
}
```

[图片详解](http://images.cnitblog.com/i/497634/201403/121755260214693.jpg)
