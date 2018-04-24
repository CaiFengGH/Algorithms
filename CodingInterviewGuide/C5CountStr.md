>题目描述

计算字符串的统计字符串；根据统计字符串，返回第index个的字符，index >= 0；

- 实现方法

```
package Chapter5;

/**
 * @author Ethan
 * @desc 获取字符串的统计字符串，如aabbc，返回a_2_b_2_c_1
 */
public class C5CountString {

	/**
	 * @author Ethan
	 * @desc 返回统计字符串中index位置的字符
	 */
	public char getCharAt(String countStr,int index){
		//1-异常参数检测
		if(countStr == null || countStr.length() == 0 || index > countStr.length() - 1){
			return 0;
		}
		//2-初始化 stage: sum: num: cur:
		char[] cha = countStr.toCharArray();
		boolean stage = true;
		int sum = 0;
		int num = 0;
		char cur = 0;
		//3-遍历
		for(int i = 0; i < cha.length; i++){
			if(cha[i] == '_'){
				stage = !stage;
			}else if(stage){
				sum = sum + num;
				if(sum > index){
					return cur;
				}
				num = 0;
				cur = cha[i];
			}else{
				num = num * 10 + cha[i] - '0';
			}
		}
		//4-异常检查
		return sum + num > index ? cur : 0;
	}
	
	/**
	 * @author Ethan
	 * @desc 获取统计字符串
	 */
	public String getCountString(String str){
		//1-异常参数检测
		if(str == null || str.length() == 0){
			return null;
		}
		//2-初始化 res: num:
		char[] cha = str.toCharArray();
		String res = String.valueOf(cha[0]);
		int num = 0;
		//3-遍历
		for(int i = 1; i < cha.length; i++){
			if(cha[i] != cha[i-1]){
				res = concat(res,num,String.valueOf(cha[i]));
				num = 1;
			}else{
				num++;
			}
		}
		//4-返回
		return concat(res,num,"");
	}

	public String concat(String res, int num, String nextCha) {
		return res + "_" + String.valueOf(num) 
				+ (nextCha.equals("") ? nextCha : "_"+nextCha);
	}
}
```
