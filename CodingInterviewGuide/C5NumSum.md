>题目描述

计算字符串中数字之和，'-'在数字之前为负，'--'在数字之前为正；

```
package Chapter5;

/**
 * @author Ethan
 * @desc 实现字符串中数字之和，'-'在数字前为负数，'--'在数字前为正数 
 */
public class C5NumSum {

	public int numSum(String str){
		//1-异常参数检测
		if(str == null || str.length() == 0){
			return 0;
		}
		//2-初始化操作 cha:字符数组 res:求和结果 num:当前数字 positive:数字正负 cur:当前字符与'0'差
		char[] cha = str.toCharArray();
		
		int res = 0;
		int num = 0;
		boolean positive = true;
		int cur = 0;
		
		//3-遍历寻找数字和求和
		for(int i = 0; i < cha.length; i++){
			cur = cha[i] - '0';
			//非数字直接求和，数字更新num
			if(cur < 0 || cur > 9){
				//求和且num归零
				res += num;
				num = 0;
				//更新positive
				if(cha[i] == '-'){
					//判断前一个字符是否为'-'
					if(i > 0 & cha[i-1] == '-'){
						//此处不能直接为true，奇数个'-'为负
						positive = !positive;
					}else{
						positive = false;
					}
				}else{
					positive = true;
				}
			}else{
				num = num * 10 + (positive == true ? cur : -cur);
			}
		}
		//4-字符串以数字结尾
		res += num;
		return res;
	}
}

```
