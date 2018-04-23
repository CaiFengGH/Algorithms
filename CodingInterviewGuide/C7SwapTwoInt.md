>题目描述

交换两个整数的值；

- 实现方法

基于异或性质： a ^ b = c | a ^ c = b | b ^ c = a

```
package Chapter7;

/**
 * @author Ethan
 * @desc 交换两个int值 
 */
public class C7SwapTwoInt {

	/**
	 * @author Ethan
	 * @desc 基于异或性质
	 */
	public void swapTwoInt(int a,int b){
		//a ^ b = c | b ^ c = a | a ^ c = b
		a = a ^ b;
		b = a ^ b;
		a = a ^ b;
	}
}

```
