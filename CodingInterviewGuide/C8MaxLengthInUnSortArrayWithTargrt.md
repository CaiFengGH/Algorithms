```
package Chapter8;

import java.util.HashMap;

/**
 * @author Ethan
 * @desc 在未排序的整数数组中返回累加和满足给定值的最长子数组长度 
 */
public class C8MaxLengthInSortArrayWithTarget {

	/**
	 * @author Ethan
	 * @desc 核心思路：arr[j...i]的和为s(i)-s(j-1)
	 */
	public int maxLength(int[] nums,int target){
		//1-异常参数
		if(nums == null || nums.length == 0){
			return -1;
		}
		//2-初始化 map:key-sum value:index sum: maxLen:
		HashMap<Integer,Integer> map = new HashMap<Integer,Integer>();
		map.put(0, -1);
		
		int sum = 0;
		int maxLen = 0;
		
		//3-遍历
		for(int i = 0; i < nums.length; i++){
			sum += nums[i];
			
			if(map.containsKey(sum - target)){
				maxLen = Math.max(i - map.get(sum - target), maxLen);
			}
			
			if(!map.containsKey(sum)){
				map.put(sum, i);
			}
		}
		return maxLen;
	}
}

```
