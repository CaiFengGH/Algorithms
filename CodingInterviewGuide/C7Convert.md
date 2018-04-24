>题目描述

将一个整数字符串转换为整数；

- 实现方法

主要分为两个问题：字符串不符合整数规范问题；整数超过32位表达范围；

1-整数规范问题：

首位不为'-'或者数字；

首位为'-'且长度仅为1，首位为'-'且下一位为'0'；

首位为'0'且长度大于1；

字符串中间有非数字字符；

2-溢出问题

32位的表达范围是-2147483648~2147483647，因为负数绝对值的表达范围高于整数，统一以负数表达；

以posi标示正负；minP标示Integer类型的最小商；minR标示Integer类型的最后一位余数；

```
package Chapter7;

/**
 * @author Ethan
 * @desc 将整数型字符串转换为整数 
 */
public class C7Convert {

	public int convert(String str){
		//1-异常参数检测
		if(str == null || str.length() == 0){
			return 0;
		}
		//2-是否符合整数规范
		char[] cha = str.toCharArray();
		boolean flag = isValid(cha);
		if(!flag){
			return 0;
		}
		
		boolean posi = cha[0] == '-' ? false : true;
		//3-最小商和最小余数
		int minP = Integer.MIN_VALUE / 10;
		int minR = Integer.MIN_VALUE % 10;
		//4-初始化 res: cur:
		int res = 0;
		int cur = 0;
		//5-遍历
		for(int i = posi ? 0 : 1; i < cha.length; i++){
			cur = '0' - cha[i];
			if(res < minP || (res == minP && cur < minR)){
				return 0;
			}
			res = res * 10 + cur; 
		}
		//6-32位最小整数的相反数溢出检测
		if(posi && res == Integer.MIN_VALUE){
			return 0;
		}
		return posi ? -res : res;
	}

	/**
	 * @author Ethan
	 * @desc 对整数型的字符串进行检测 
	 */
	public boolean isValid(char[] cha) {
		//1-首位为'-'或者数字
		if(cha[0] != '-' && (cha[0] < '0' || cha[0] > '9') ){
			return false;
		}
		//2-首位为'-'且长度为1，或者首位为'-'且下一位为0
		if(cha[0] == '-' && (cha.length == 1 || cha[1] == '0')){
			return false;
		}
		//3-首位为0且长度为1
		if(cha[0] == '0' && cha.length > 1){
			return false;
		}
		//3-字符串中间有非数字
		for(int i = 1; i < cha.length; i++){
			if((cha[i] < '0' || cha[i] > '9') ){
				return false;
			}
		}
		return true;
	}
}

```
