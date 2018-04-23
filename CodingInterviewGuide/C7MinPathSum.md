>题目描述

返回矩阵中最短路径和；

- 实现方法

基于经典动态规划算法，理解简单，时间复杂度为O(M*N)，空间复杂度为O(M*N)；

基于压缩的动态规划算法，实现滚动更新，时间复杂度不变，空间复杂度为O(min(M*N))；

```
package Chapter7;

/**
 * @author Ethan
 * @desc 返回矩阵的最小路径和 
 */
public class C7MinPathSum {

	/**
	 * @author Ethan
	 * @desc 经典的动态规划算法
	 */
	public int minPathSum1(int[][] m){
		//1-异常参数检测
		if(m == null || m[0] == null || m.length == 0 || m[0].length == 0){
			return 0;
		}
		//2-初始化行列
		int rows = m.length;
		int cols = m[0].length;
		//3-初始化dp数组
		int[][] dp = new int[rows][cols];
		dp[0][0] = m[0][0];
		
		for(int i = 1; i < cols; i++){
			dp[0][i] = dp[0][i-1] + m[0][i];
		}
		
		for(int j = 1; j < rows; j++){
			dp[j][0] = dp[j-1][0] + m[j][0];
		}
		//4-按照动态方程移动
		for(int k = 1; k < rows; k++){
			for(int l = 1; l < cols; l++){
				dp[k][l] = Math.min(dp[k-1][l], dp[k][l-1]) + m[k][l];
			}
		}
		return dp[rows - 1][cols - 1];
	}
	
	/**
	 * @author Ethan
	 * @desc 基于压缩的动态规划算法，辅助数组的长度为行列较小值
	 */
	public int minPathSum2(int[][] m){
		//1-异常参数检测
		if(m == null || m[0] == null || m.length == 0 || m[0].length == 0){
			return 0;
		}
		
		//2-初始化较大值和较小值
		int large = m.length > m[0].length ? m.length : m[0].length;
		int small = m.length > m[0].length ? m[0].length : m.length;
		
		//3-flag行列中较大者
		boolean rowLarge = large == m.length;
		
		//4-初始复制
		int[] dp = new int[small];
		dp[0] = m[0][0];
		
		for(int i = 1; i < small; i++){
			dp[i] = dp[i-1] + (rowLarge ? m[0][i] : m[i][0]);
		}
		
		//5-按照较大者方向移动
		for(int j = 1; j < large; j++){
			dp[0] = dp[0] + (rowLarge ? m[j][0] : m[0][j]) ;
			for(int k = 1; k < small; k++){
				dp[k] = Math.min(dp[k-1], dp[k]) + (rowLarge ? m[j][k] : m[k][j]);
			}
		}
		return dp[small - 1];
	}
}
```
