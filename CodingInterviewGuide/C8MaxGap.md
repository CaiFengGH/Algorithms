```
package Chapter8;

/**
 * @author Ethan
 * @desc 数组排序后相连值的最大差值 
 */
public class C8MaxGap {

	/**
	 * @author Ethan
	 * @desc 结合桶排序思路
	 */
	public int maxGap(int[] num){
		//1-异常参数检测
		if(num == null || num.length < 2){
			return 0;
		}
		//2-数组中最大值和最小值 max min
		int len = num.length;
		int max = Integer.MIN_VALUE;
		int min = Integer.MAX_VALUE;
		for(int i = 0; i < len; i++){
			min = Math.min(min, num[i]);
			max = Math.max(max, num[i]);
		}
		if(min == max){
			return 0;
		}
		//3-初始化数组 maxs mins hasNum
		boolean[] hasNum = new boolean[len + 1];
		int[] maxs = new int[len + 1];
		int[] mins = new int[len + 1];
		int bucket = 0;
		
		//4-遍历赋值
		for(int i = 0; i < len; i++){
			//计算桶序号
			bucket = bucIndex(num[i],len,max,min);
			mins[bucket] = hasNum[bucket] ? Math.min(mins[bucket], num[i]) : num[i];
			maxs[bucket] = hasNum[bucket] ? Math.max(maxs[bucket], num[i]) : num[i];
			hasNum[bucket] = true;
		}
		
		//5-找到第一个非空桶的最大值
		int lastMax = 0;
		int res = 0;
		int i = 0;
		
		while(i <= len){
			if(hasNum[i++]){
				lastMax = maxs[i - 1];
				break;
			}
		}
		//6-最大gap来源于相邻两个非空桶的后者最小值与前者最大值的差
		for(; i <= len; i++){
			if(hasNum[i]){
				res = Math.max(res, mins[i] - lastMax);
				lastMax = maxs[i];
			}
		}
		return res;
	}

	/**
	 * @author Ethan
	 * @desc 返回桶索引 
	 */
	private int bucIndex(int num, int len, int max, int min) {
		return (num - min) * len / (max - min);
	}
	
	public static void main(String[] args) {
		C8MaxGap mg = new C8MaxGap();
		int[] num = {5,5,5,5};
		int res = mg.maxGap(num);
		System.out.println(res);
	}
}
```
