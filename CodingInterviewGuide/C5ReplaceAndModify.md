>题目描述

替换字符串中内容；将空格全部替换为%20，将12**345 转换为 **12345；

- 实现方法

从后往前遍历，比较和赋值；

```
package Chapter5;

/**
 * @author Ethan
 * @desc 
 * 1-将字符串str中的空格替换为%20
 * 2-将数字中的所有*号移动到最左边 
 */
public class C5ReplaceAndModify {
	
	public void replace(char[] cha){
		//1-异常参数检测
		if(cha == null || cha.length == 0){
			return ;
		}
		//2-初始化 len: num:
		int len = 0;
		int num = 0;
		for(len = 0; len < cha.length && cha[len] != 0; len++){
			if(cha[len] == ' '){
				num++;
			}
		}
		//3-替换操作
		int j = len + 2 * num - 1;
		for(int i = len - 1; i > -1;i--){
			//从后往前遍历，非空格移动，空格替换
			if(cha[i] != ' '){
				cha[j--] = cha[i];
			}else{
				cha[j--] = '0';
				cha[j--] = '2';
				cha[j--] = '%';
			}
		}
	}
	
	/**
	 * @author Ethan
	 * @desc 12**345 **12345
	 */
	public void modify(char[] cha){
		//1-异常参数检测
		if(cha == null || cha.length == 0){
			return ;
		}
		//2-遍历移动
		int j = cha.length - 1;
		for(int i = cha.length - 1; i > -1; i--){
			if(cha[i] != '*'){
				cha[j--] = cha[i];
			}
		}
		//3-统一赋值为*
		for(;j > -1;){
			cha[j--] = '*';
		}
	}
}
```
