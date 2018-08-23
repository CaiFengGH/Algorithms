```
package Chapter4;

/**
 * @author Ethan
 * @desc 返回数组的最长递增子序列 
 */
public class C4LongestIncreaseSeq {

	public int[] lis(int[] nums){
		//1-异常参数检测
		if(nums == null || nums.length == 0){
			return null;
		}
		//2-获取dp数组
		int[] dp = getDp(nums);
		//3-生成lis数组
		return generateLis(nums,dp);
	}

	/**
	 * @author Ethan
	 * @desc 由数组和dp返回最长递增子序列
	 */
	private int[] generateLis(int[] nums, int[] dp) {
		//1-初始化 len: index:
		int len = 0;
		int index = 0;
		//2-寻找最长值的索引
		for(int i = 0; i < nums.length; i++){
			if(nums[i] > len){
				len = nums[i];
				index = i;
			}
		}
		//3-初始化res
		int[] res = new int[len];
		res[--len] = nums[index];
		
		//4-遍历返回最终结果
		for(int i = index; i >= 0; i--){
			//值小且对应的dp小1
			if(nums[i] < nums[index] && dp[i] == dp[index] - 1){
				res[--len] = nums[i];
				index = i;
			}
		}
		return res;
	}

	/**
	 * @author Ethan
	 * @desc 生成dp数组
	 */
	private int[] getDp(int[] nums) {
		int[] dp = new int[nums.length];
		for(int i = 0; i < nums.length; i++){
			dp[i] = 1;
			for(int j = 0; j < i; j--){
				if(nums[i] > nums[j]){
					dp[i] = Math.max(dp[i], dp[j] + 1);
				}
			}
		}
		return dp;
	}
}
```
