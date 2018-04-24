>题目描述

替换字符串中重复出现的字符串；

- 实现方法

str：原始字符串 from：被替换字符串 to：替换为字符串

使用match来记录匹配到from的什么位置；

```
package Chapter5;

/**
 * @author Ethan
 * @desc 替换字符串中重复出现的字符
 */
public class C5Replace {

	public String replace(String str,String from,String to){
		//1-异常参数检测
		if(str == null || str.length() == 0){
			return null;
		}
		//2-将重复字符替换为0
		char[] chaStr = str.toCharArray();
		char[] chaFrom = from.toCharArray();
		int match = 0;
		
		for(int i = 0 ; i < chaStr.length ; i++){
			if(chaStr[i] == chaFrom[match++]){
				if(match == chaFrom.length){
					clean(chaStr,i,chaFrom.length);
					match = 0;
				}
			}else{
				if(chaStr[i] == chaFrom[0]){
					i--;
				}
				match = 0;
			}
		}
		//3-将连0替换为to
		String res = "";
		String cur = "";
		for(int i = 0; i < chaStr.length; i++){
			if(chaStr[i] != 0){
				cur = cur + String.valueOf(chaStr[i]);
			}
			if(chaStr[i] == 0 && (i == 0 || chaStr[i-1] != 0)){
				res = res + cur + to;
				cur = "";
			}
		}
		if(!cur.equals("")){
			res = res + cur;
		}
		return res;
	}

	/**
	 * @author Ethan
	 * @desc 将字符数组中的部分元素置为0
	 */
	public void clean(char[] chaStr, int end, int len) {
		while(len > 0){
			chaStr[end--] = 0;
			len--;
		}
	}
}
```
