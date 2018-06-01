```
package Chapter4;

/**
 * @author Ethan
 * @desc 给定数组arr，数组中为钱币且不重复，
 * 指定换钱的总数aim，返回换钱的最少货币数
 */
public class C4MinCost {

	/**
	 * @author Ethan
	 * @desc 返回还钱的最小货币数，没有返回-1 
	 */
	public int minCost(int[] arr,int aim){
		//1-异常参数检测
		if(arr == null || arr.length == 0 || aim <= 0){
			return -1;
		}
		//2-初始化 n:币种个数 dp:n行aim+1列
		int n = arr.length;
		
		//dp数组的第一列全为0
		int[][] dp = new int[n][aim + 1];
		int max = Integer.MAX_VALUE;
		
		//3-初始化第一行，arr[0]的整数倍的索引值不断加1
		
		for(int i = 1;i <= aim; i++){
			dp[0][i] = max;
			if(i >= arr[0] && dp[0][i - arr[0]] != max){
				dp[0][i] = dp[0][i - arr[0]] + 1;
			}
		}
		
		//4-初始化剩余元素
		int left = 0;
		for(int i = 1; i < n; i++){
			for(int j = 1; j <= aim; j++){
				left = max;
				if(j >= arr[i] && dp[i][j - arr[i]] != max){
					left = dp[i][j - arr[i]] + 1;
				}
				dp[i][j] = Math.min(left,dp[i-1][j]);
			}
		}
		//根据dp动态数组的最右下角
		return dp[n-1][aim] != max ? dp[n-1][aim] : -1;
	}
}
```
