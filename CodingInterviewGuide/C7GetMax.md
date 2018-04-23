>题目描述

在不使用条件判断符的前提下，返回两者中的较大值；

- 实现方法

若ab异号，a为0或正数，返回a；a为负数，返回b；

若ab同号，a-b为0或正数，返回a；a-b为负数，返回b；

```
package Chapter7;

/**
 * @author Ethan
 * @desc 不用条件运算符判断两个数大小，返回较大值 
 */
public class C7GetMax {

	/**
	 * @author Ethan
	 * @desc 返回a和b中较大值
	 */
	public int getMax(int a,int b){
		//判断符号 a: b: c:c=a-b
		int c = a - b;
		int sa = sign(a);
		int sb = sign(b);
		int sc = sign(c);
		//判断a b是否同号:
		int diffSab = sa ^ sb;
		int sameSab = flip(diffSab);
		//ab异号则取决于a符号 ab同号则取决于c的符号
		int returnA = diffSab * sa + sameSab * sc;
		int returnB = flip(returnA);
		return a * returnA + b * returnB; 
	}
	
	/**
	 * @author Ethan
	 * @desc 0和正数:1 负数:0
	 */
	public int sign(int n){
		return flip( (n >>> 31) & 1);
	}

	private int flip(int i) {
		return i ^ 1;
	}
	
}
```
