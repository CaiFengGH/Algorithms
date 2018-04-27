>题目描述

返回字符串索引位置为k处的新字符，新字符定义为：长度为1的小写字母，长度为2的大写小写和大写大写；

- 实现方法

从k-1位置向左遍历，遇到第一个小写字母停止，计算中间个数num，num为奇数，则取k-1和k，

偶数，判断k位置是大写或者小写，大写返回k和k+1，小写直接返回；

```
package Chapter5;

/**
 * @author Ethan
 * @desc 指向新字符，新字符指长度为1或2，1：小写字母 2：大写字母和小写字母 3：大写字母和大写字母 
 */
public class C5PointNewChar {

	/**
	 * @author Ethan
	 * @desc 返回索引为k的位置上的新字符
	 */
	public String newChar(String str,int k){
		//1-异常参数检测
		if(str == null || str.length() == 0 || k < 0 || k >= str.length()){
			return null;
		}
		//2-从k-1往前遍历，直到遇到小写字母，计算中间数量num
		char[] cha = str.toCharArray();
		int num = 0;
		for(int i = k - 1; i > -1; i--){
			if(!Character.isUpperCase(cha[i])){
				break;
			}
			num++;
		}
		//3-三种类型 num:old num:even
		if((num & 1) == 1){
			return str.substring(k-1,k+1);
		}
		if(Character.isUpperCase(cha[k])){
			return str.substring(k, k+2);
		}
		return str.substring(k);
	}
}
```
