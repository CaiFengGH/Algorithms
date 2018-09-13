```
package Chapter8;

/**
 * @author Ethan
 * @desc 返回矩阵中子矩阵的最大累加和 
 */
public class C8MaxSumInMatrix {

	/**
	 * @author Ethan
	 * @desc 基于数组的子数组最大累加和问题的思路
	 */
	public int maxSum(int[][] m){
		
		//1-异常参数监测
		if(m == null || m.length == 0 || m[0].length == 0){
			System.out.println("数组不合法");
			return -1;
		}
		
		//2-初始化长度 最大值
		int rows = m.length;
		int cols = m[0].length;
		int max = Integer.MIN_VALUE;
		
		//3-初始化
		int[] s = null;
		int cur = 0;
		
		//4-依次每轮遍历
		for(int i = 0; i < rows; i++){
			//每一轮遍历
			s = new int[cols];
			for(int j = i; j < rows; j++){
				cur = 0;
				for(int k = 0; k < cols; k++){
					s[k] += m[j][k];
					cur += s[k];
					max = Math.max(max, cur);
					cur = cur <= 0 ? 0 : cur;
				}
			}
		}
		//5-基于数组的子数组最大累加和问题的思路
		return max;
	}
	
	public static void main(String[] args) {
		C8MaxSumInMatrix ms = new C8MaxSumInMatrix();
		int[][] m = {{-90,48,78},{64,-40,64},{-81,-7,66}};
		int res = ms.maxSum(m);
		System.out.println("最大和："+ res);
	}
}
```
