- 题目

用[1,5,10,20,50,100]组合出一定数目的金额，问共有多少种组合方法？

关键：币种和总量是两个分类；将币种以数组索引的方式表示；

链接：[动态规划之找钱问题](https://www.cnblogs.com/little-YTMM/p/5372680.html)

```
package DayCode;

/**
 * @author Ethan
 * @desc 用[1,5,10,20,50,100]组合出一定数目的金额，问共有多少种组合方法？
 */
public class Charge {
	
	/**
	 * @author Ethan
	 * @desc 动态规划的方式 
	 */
	public int numOfCharge(int[] money,int amount){
		int rows = money.length;
		int cols = amount + 1;
		
		int[][] dp = new int[rows][cols];
		
		//1-初始化第一行，用1元组成任何总量
		for(int i = 0; i < cols; i++){
			dp[0][i] = 1;
		}
		
		//2-初始化dp数组
		for(int j = 1; j < rows; j++){
			//任何钱币构成0元的组合默认为1
			dp[j][0] = 1;
			for(int k = 1; k < cols; k++){
				if(k < money[j]){
					dp[j][k] = dp[j - 1][k];
				}else{
					dp[j][k] = dp[j-1][k] + dp[j][k - money[j]];
				}
			}
		}
		return dp[rows - 1][cols - 1];
	}
}
```
