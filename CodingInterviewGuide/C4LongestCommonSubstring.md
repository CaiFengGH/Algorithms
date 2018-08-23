```
package Chapter4;

/**
 * @author Ethan
 * @desc 返回最长公共子字符串 
 */
/**
 * @author Ethan
 * @desc 
 */
public class C4LongestCommonSubstring {
	
	public String lcs(String str1,String str2){
		//1-异常参数检测
		if(str1 == null || str2 == null || 
				str1.length() == 0 || str2.length() == 0){
			return null;
		}
		//2-初始化
		char[] cha1 = str1.toCharArray();
		char[] cha2 = str2.toCharArray();
		//3-获取dp数组
		int[][] dp = getDp(cha1,cha2);
		//4-遍历寻找最大值
		int end = 0;
		int max = 0;
		
		for(int i = 0; i < cha1.length; i++){
			for(int j = 0; j < cha2.length; j++){
				if(dp[i][j] > max){
					end = i;
					max = dp[i][j];
				}
			}
		}
		return str1.substring(end - max + 1,end);
	}

	/**
	 * @author Ethan
	 * @desc 生成dp数组 
	 */
	private int[][] getDp(char[] cha1, char[] cha2) {
		//1-初始化
		int[][] dp = new int[cha1.length][cha2.length];
		//2-初始化
		for(int i = 0; i < cha1.length; i++){
			if(cha1[i] == cha2[0]){
				dp[i][0] = 1;
			}
		}
			
		for(int j = 1; j < cha2.length; j++){
			if(cha2[j] == cha1[0]){
				dp[0][j] = 1;
			}
		}
		
		for(int k = 1; k < cha1.length; k++){
			for(int l = 1; k < cha2.length; k++){
				if(cha1[k] == cha2[l]){
					dp[k][l] = dp[k-1][l-1] + 1;
				}
			}
		}
		
		return dp;
	}
}
```
