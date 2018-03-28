>题目描述

判断两个字符串是否是变形词，变形词指两个词字符种类和每个字符频率相等；

```
package Chapter5;

/**
 * @author Ethan
 * @desc 判断两个字符串是否为变形词 
 * 变形词:字符出现的种类和频率相同
 */
public class C5IsDeformation {

	public boolean isDeformation(String str1,String str2){
		//1-异常参数判断
		if(str1 == null || str2 == null || str1.length() != str2.length()){
			return false;
		}
		//2-初始化map数组，数组大小为ASCII编码大小
		int[] map = new int[256];
		int temp = 0;
		
		char[] cha1 = str1.toCharArray();
		char[] cha2 = str2.toCharArray();
		//3-根据str1赋值给map
		for(int i = 0; i < cha1.length; i++){
			map[cha1[i]]++;
		}
		//4-根据str2赋值给map
		for(int i = 0; i < cha2.length; i++){
			//注意自加和自减运算和操作的优先顺序
			temp = map[cha2[i]]--; 
			if( temp < 0){
				return false;
			}
		}
		return true;
	}
}

```
