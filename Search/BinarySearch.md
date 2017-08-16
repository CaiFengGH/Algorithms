>二分查找

- 查找原理

将数组分为三部分，中值前，中值，中值后，目标值与中值比较，大于则其位于中值后区间，小于则其位于中值前区间；

对新的区间进行不断迭代，直至找到目标值为止；

- 注意事项

二分查找的时间复杂度为O(lgN);

二分查找的前提是数组有序排列；

```
/**
 * @author Ethan
 * @desc 二分查找 注意：前提必须是有序数组
 * @date 2017年8月16日
 */
public class BinarySearch {
	
	/**
	 * @desc 基于循环的二分查找
	 * @param arr 数组
	 * @param target 目标值
	 * @return 目标值所在索引 -1:代表不存在
	 */
	public static int binarySearch1(int[] arr,int target){
		int left = 0;
		int right = arr.length - 1;
		int middle = (left + right) / 2;
		
		while(left <= right){
			if(target == arr[middle]){
				return middle;
			}else if(target < arr[middle]){
				right = middle - 1;
			}else{
				left = middle + 1;
			}
			middle = (left + right) / 2;
		}
		return -1;
	}
	
	/**
	 * @desc 基于迭代的二分查找
	 * @param arr 数组
	 * @param left 左边界
	 * @param right 右边界
	 * @param target 关键值
	 * @return 目标值所在索引 -1:代表不存在
	 */
	public static int binarySearch2(int[] arr,int left,int right,int target){
		if(target < arr[left] || target > arr[right]){
			return -1;
		}
		
		int middle = (left + right) / 2;
		
		if(target < arr[middle]){
			return binarySearch2(arr,0,middle - 1,target);
		}else if(target > arr[middle]){
			return binarySearch2(arr,middle + 1,right,target);
		}else{
			return middle;
		}
	}
}
```
