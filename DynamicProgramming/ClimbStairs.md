```
package DayCode;

/**
 * @author Ethan
 * @desc 动态规划爬楼梯问题 
 */
public class ClimbStairs {

	/**
	 * @author Ethan
	 * @desc 每次只能爬一步或者两步，有多少种方案
	 */
	public int climbStairs(int n){
		//1-初始化操作 res[n]:爬n阶台阶有多少种可能
		int[] res = new int[n+1];
		res[0] = 0;
		//2-n的情况判断
		if(n > 0){
			res[1] = 1;
		}
		if(n > 2){
			res[2] = 2;
		}
		if(n >= 3){
			for(int i = 3; i <= n; i++){
				res[i] = res[i - 1] + res[i - 2];
			}
		}
		return res[n];
	}
}

```
