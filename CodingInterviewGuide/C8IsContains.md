```
package Chapter4;

/**
 * @author Ethan
 * @desc 在行列都排序的数组中判断肯定值是否存在
 * 时间复杂度为O(N+M)，空间复杂度为O(1) 
 */
public class C4IsContains {

	/**
	 * @author Ethan
	 * @desc num:给定数组 k:目标值
	 * num行列均是有序的
	 */
	public boolean isContains(int[][] num,int k){
		//1-异常参数检测
		if(num == null || num.length == 0 || num[0].length == 0){
			return false;
		}
		//2-初始化右上角位置
		int rows = num.length;
		int col = num[0].length - 1; 
		int row = 0;
		
		//3-循环比较移动
		while(row < rows && col > -1){
			if(num[row][col] == k){
				return true;
			}else if(num[row][col] < k){
				row++;
			}else{
				col--;
			}
		}
		//4-循环未确定
		return false;
	}
}
```
