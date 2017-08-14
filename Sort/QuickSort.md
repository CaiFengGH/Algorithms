>快速排序

- 工作原理

选择一个基准数，通常为数据左侧，一次遍历，将数据分为两个部分，前面部分小于基准数，后面部分大于基准数；

采用分治策略，分别对前后两部分数据进行遍历，直到所有数据有序排列；

- 注意事项

快速排序的时间复杂度为O(N*lgN)，最坏时间复杂度为O(N*N);

快速排序是不稳定的算法，排序前相等的两个数的位置会发生变化；


```
/**
 * @author Ethan
 * @desc 用于实现快速排序
 * @date 2017年8月14日
 */
public class QuickSort {
	/**
	 * @desc 快速排序
	 * @param arr 数组
	 * @param left 左边界
	 * @param right 右边界
	 */
	public void quickSort(int[] arr,int left,int right){
		//分支递归的判决条件
		if(left < right){
			//记录左右边界和基准值
			int i = left;
			int j = right;
			int v = arr[i];
			//进行遍历选择，前面均小于基准值，后面均大于基准值
			while(i < j){
				//从右往左选择小于基准值的值
				while(i < j && arr[j] > v){
					j--;
				}
				//不满足此条件，即右侧值均大于基准值，无需赋值
				if(i < j){
					arr[i++] = arr[j];
				}
				//从左往右选择大于基准值的值
				while(i < j && arr[i] < v){
					i++;
				}
				if(i < j){
					arr[j--] = arr[i];
				}
			}
			arr[i] = v;
			//左右分治
			quickSort(arr,left,i-1);
			quickSort(arr,i+1,right);
		}
	}
}
```

[图片详解](http://images.cnitblog.com/i/497634/201403/121659127078460.jpg)
