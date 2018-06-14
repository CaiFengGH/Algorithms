```
package Chapter9;

/**
 * @author Ethan
 * @desc 判断一个整数是否是回文整数 
 */
public class C9IntIsPalindrome {
	
	/**
	 * @author Ethan
	 * @desc 基于正数进行判断
	 */
	public boolean intIsPalindrome(int n){
		
		//1-异常参数判断，最小-2147483648
		if(n == Integer.MIN_VALUE){
			return false;
		}
		
		//2-初始化help 和 n相同位数的10的次幂
		n = Math.abs(n);
		int help = 1;
		while(n / help >= 10){
			help = help * 10;
		}
		
		//3-循环剔除左右n的第一位和最后一位
		while(n != 0){
			if((n / help) != (n % 10)){
				return false;
			}
			//此处同时去除首位和最后一位
			n = (n % help) / 10;
			help = help / 100;
		}
		return true;
	}
}

```
