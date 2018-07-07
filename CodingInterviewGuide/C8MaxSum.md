```
package Chapter8;

/**
 * @author Ethan
 * @desc 子数组的最大累加和问题 
 */
public class C8MaxSum {

	/**
	 * @author Ethan
	 * @desc 子数组的最大累加和
	 * 如果全负，则负值中的最大值
	 * 如果有正，当前和cur为负则更新为0
	 */
	public int maxSum(int[] arr){
		//1-异常参数检测 
		if(arr == null || arr.length == 0){
			return 0;
		}
		//2-初始化 cur:当前和 max:最大值
		int cur = 0;
		int max = Integer.MIN_VALUE;
		//3-遍历求和寻找最大值
		for(int i = 0; i < arr.length; i++){
			cur += arr[i];
			max = Math.max(max,cur);
			cur = cur < 0 ? 0 : cur;
		}
		return max;
	}
	
	public static void main(String[] args) {
		C8MaxSum c8 = new C8MaxSum();
		//1-全为负
		int[] arr1 = {-3,-2,-1,-5};
		//2-有正有负
		int[] arr2 = {1,-2,3,-5};
		int res = c8.maxSum(arr2);
		System.out.println(res);
	}
}

```
