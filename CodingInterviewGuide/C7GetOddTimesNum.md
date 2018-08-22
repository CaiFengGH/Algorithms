```
package Chapter7;

public class C7GetOddTimesNum {

	/**
	 * @author Ethan
	 * @desc 所有数字出现偶数次，两个数字出现奇数次 
	 */
	public void getOddTimeNum(int[] nums){
		//1-初始化 res: one:
		int midRes = 0;
		int one = 0;
		int res = 0;
		
		for(int i : nums){
			midRes ^= i;
		}
		//2-找出某一位bit不一样的情况
		one = midRes & (-midRes);
		System.out.println(one);
		
		for(int j : nums){
			if((j & one) != 0){
				res ^= j;
			}
		}
		System.out.println(res + "-" + (res ^ midRes));
	}
}
```
