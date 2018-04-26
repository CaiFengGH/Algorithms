>题目描述

返回两个字符串的最长公共子序列；

- 实现方法

基于经典动态规划算法，求解dp数组；

从dp最右下角元素依次向上/向左/向左上角移动，利用res数组记录向左上角移动时的元素；

```
package Chapter7;

/**
 * @author Ethan
 * @desc 返回两个数组的最长公共子序列 
 */
public class C7LongestCommonSeq {

	public String longestCommonSeq(String str1,String str2){
		//1-异常参数检测
		if(str1 == null || str2 == null || str1.length() == 0 || str2.length() == 0){
			return null;
		}
		
		//2-转换为字符数组
		char[] cha1 = str1.toCharArray();
		char[] cha2 = str2.toCharArray();
		int m = cha1.length - 1;
		int n = cha2.length - 1;
		
		//3-获取dp数组
		int[][] dp = getDp(cha1,cha2);
		
		//4-初始化结果数组
		char[] res = new char[dp[m][n]];
		int index = res.length - 1;
		
		//5-移动复制初始化数组
		while(index >= 0){
			if(n > 0 && dp[m][n] == dp[m][n-1]){
				n--;
			}else if(m > 0 && dp[m][n] == dp[m-1][n]){
				m--;
			}else{
				res[index--] = cha1[m];
				m--;
				n--;
			}
		}
		return String.valueOf(res);
	}
	
	/**
	 * @author Ethan
	 * @desc 经典动态规划中的dp 
	 */
	public int[][] getDp(char[] cha1,char[] cha2){
		//1-初始化dp维度 m: n:
		int m = cha1.length;
		int n = cha2.length;
		//2-初始化dp
		int[][] dp = new int[m][n];
		dp[0][0] = cha1[0] == cha2[0] ? 1 : 0;
		//3-赋值dp第一行和第一列
		for(int i = 1; i < m; i++){
			//三元运算符
			dp[i][0] = Math.max(dp[i-1][0], cha1[i] == cha2[0] ? 1 : 0);
		}
		
		for(int j = 1; j < n; j++){
			dp[0][j] = Math.max(dp[0][j-1], cha2[j] == cha1[0] ? 1 : 0);
		}
		//4-循环赋值dp
		for(int i = 1; i < m;i++){
			for(int j = 1; j < n;j++){
				dp[i][j] = Math.max(dp[i-1][j], dp[i][j-1]);
				if(cha1[i] == cha2[j]){
					dp[i][j] = Math.max(dp[i][j], dp[i-1][j-1] + 1);
				}
			}
		}
		return dp;
	}
}
```
