>归并排序

- 排序原理

归并排序主要分为分解和合并操作；

递归的将当前区间分为子空间，直至子空间大小为1；

递归的将子空间不断合并成有序的子空间，直至生成有序的空间；

- 注意事项

归并排序的时间复杂度为O(N*lgN);

```
/**
 * @author Ethan
 * @desc 实现归并排序
 * @date 2017年8月15日
 */
public class MergeSort {
	/**
	 * @desc 归并之分解  
	 * @param arr 数组
	 * @param left 左边界
	 * @param right 右边界
	 */
	public void divideGroup(int[] arr,int left,int right){
		//递归进行条件
		if(left < right){
			int mid = (left + right) / 2;
			divideGroup(arr,left,mid);
			divideGroup(arr,(mid+1),right);
			mergeSort(arr,left,mid,right);
		}
	}

	/**
	 * @desc 归并之合并
	 * @param arr 数组
	 * @param left 左边界
	 * @param mid 中间
	 * @param right 右边界
	 */
	public void mergeSort(int[] arr, int left, int mid, int right) {
		//用于拷贝临时数组中的元素
		//初始化临时数组和其索引
		int[] temp = new int[arr.length];
		int index = left;
		int index2 = left;
		
		//初始化中心元素，center=mid+1
		int center = mid + 1;
		
		//合并前两分组左右两侧比较赋值
		while(left <= mid && center <= right){
			if(arr[left] > arr[center]){
				temp[index++] = arr[center++];
			}else{
				temp[index++] = arr[left++];
			}
		}
		//两侧比较赋值后仍有一侧存在未赋值元素
		//实现右侧剩余赋值
		while(center <= right){
			temp[index++] = arr[center++];
		}
		//实现左侧剩余赋值
		while(left <= mid){
			temp[index++] = arr[left++];
		}
		//将临时数组完全拷贝到原数组中
		while(index2 <= right){
			arr[index2] = temp[index2++];
		}
	}
}
```

[图片理解](http://images.cnitblog.com/i/497634/201403/151853346211212.jpg)
