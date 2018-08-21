```
package Chapter8;

/**
 * @author Ethan
 * @desc 返回未排序正数数组中累加和满足给定值的最大子数组长度 
 */
public class C8MaxLengthInUnsortPosArrayWithTarget {

	/**
	 * @author Ethan
	 * @desc 子数组最大值
	 */
	public int maxLength(int[] nums,int target){
		//1-异常参数检测
		if(nums == null || nums.length == 0 || target <= 0){
			return -1;
		}
		//2-初始化 left: right: sum: maxLen:
		int left = 0;
		int right = 0;
		int sum = 0;
		int maxLen = 0;
		//3-遍历
		while(right < nums.length){
			
			if(sum == target){
				maxLen = Math.max(right - left + 1, maxLen);
				sum -= nums[left++];
			}
			else if(sum < target){
				right++;
				if(right >= nums.length){
					break;
				}
				sum += nums[right];
			}
			else{
				sum -= nums[left++];
			}
		}
		return maxLen;
	}
}
```
