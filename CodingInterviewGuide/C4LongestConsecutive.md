>题目描述

给定数组，返回其中连续最长子序列的长度

- 实现方法

初始化HashMap，key：元素值，value：元素在其连续序列的长度；

从前往后遍历，每次只添加前面未出现的元素；

判断map中是否包含该元素的左右相邻元素，如果有则合并两个连续子序列，且更新新序列的左右元素的value值；

```
package Chapter4;

import java.util.HashMap;

/**
 * @author Ethan
 * @desc 返回无序数组中最长连续子序列的长度 
 */
public class C4LongestConsecutive {

	public int longestConsecutive(int[] arr){
		//1-异常参数检测
		if(arr == null || arr.length == 0){
			return 0;
		}
		//2-初始化 map:key为值 value:值所在序列的长度 max:最大长度 hashmap存储元素唯一
		HashMap<Integer,Integer> map = new HashMap<Integer, Integer>();
		int max = 0;
		//3-循环遍历
		for(int i = 0 ; i < arr.length; i++){
			//只添加前面未出现元素
			if(!map.containsKey(arr[i])){
				map.put(arr[i], 1);
				if(map.containsKey(arr[i] - 1)){
					max = merge(map,arr[i] - 1,arr[i]);
				}
				if(map.containsKey(arr[i] + 1)){
					max = merge(map, arr[i], arr[i] + 1);
				}
			}
		}
		//4-返回值
		return max;
	}

	/**
	 * @author Ethan
	 * @desc 合并两个连续子序列
	 */
	private int merge(HashMap<Integer,Integer> map, int small, int large) {
		int left = small - map.get(small) + 1;
		int right = large + map.get(large) - 1;
		int len = right - left + 1;
		//此处仅更新合并成的新序列的左右边界
		map.put(left, len);
		map.put(right, len);
		return len;
	}
}
```
