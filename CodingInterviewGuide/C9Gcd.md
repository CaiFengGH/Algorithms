```
package Chapter9;

/**
 * @author Ethan
 * @desc 一行代码求解最大公约数 
 */
public class C9Gcd {

	/**
	 * @author Ethan
	 * @desc m除以n的商和余数分别为p和r，m=pn+r，
	 * 则m和n的最大公约数等于n和r的最大公约数
	 */
	public int gcd(int m,int n){
		//欧几里得算法
		return n == 0 ? m : gcd(n,m % n);
	}
}

```
