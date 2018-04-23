>题目描述

基于位运算实现加减法；

- 实现方法

不基于进位的相加：取异或操作；仅基于进位的相加：取相与操作；

一个数的相反数为各位取反加1（使用补码储存）；

```
package Chapter7;

/**
 * @author Ethan
 * @desc 基于位运算实现加减法 
 */
public class C7AddMinus {

	public int add(int a,int b){
		int sum = a;
		while(b != 0){
			sum = a ^ b;
			b = (a & b) << 1;
			a = sum;
		}
		return sum;
	}
	
	public int minus(int a,int b){
		return add(a,negNum(b));
	}

	/**
	 * @author Ethan
	 * @desc 一个数取反加1 
	 */
	private int negNum(int b) {
		return ~b + 1;
	}
}

```
