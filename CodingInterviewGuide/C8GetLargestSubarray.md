```
package Chapter8;

import java.util.HashSet;

/**
 * @author Ethan
 * @desc 获取最大的可整合数组的长度 
 * 可整合数组：排序后相邻元素的差的绝对值为1
 */
public class C8GetLargestSubarray {

	/**
	 * @author Ethan
	 * @desc 返回最大的可整合数组长度
	 */
	public int getLargestSubarray(int[] arr){
		//1-异常参数检测
		if(arr == null || arr.length == 0){
			return 0;
		}
		
		//2-初始化 len:长度 max:最大值 min:最小值 set:每个数组元素值
		int len = 0;
		int max = 0;
		int min = 0;
		HashSet<Integer> set = new HashSet<Integer>();
		int arrLen = arr.length;
		
		//3-双重循环
		for(int i = 0; i < arrLen; i++){
			max = Integer.MIN_VALUE;
			min = Integer.MAX_VALUE;
			//一次循环
			for(int j = i; j < arrLen; j++){
				//存在重复元素直接break
				if(set.contains(arr[j])){
					break;
				}
				set.add(arr[j]);
				max = Math.max(max, arr[j]);
				min = Math.min(min, arr[j]);
				//4-判断是否是可整合数组
				if(max - min == j - i){
					len = Math.max(len,j - i + 1);
				}
			}
			set.clear();
		}
		return len;
	}
}
```
