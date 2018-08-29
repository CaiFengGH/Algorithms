```
package Chapter9;

public class C9Kmp {

	/**
	 * @author Ethan
	 * @desc 字符串匹配算法
	 */
	public int getIndexOf(String str,String match){
		//1-异常参数检测
		if(str == null || match == null || match.length() < 1 
				|| str.length() < match.length()){
			return -1;
		}
		
		//2-初始化
		char[] strChar = str.toCharArray();
		char[] matchChar = match.toCharArray();
		
		int strIndex = 0;
		int matchIndex = 0;
		
		int[] next = nextArr(matchChar);
		
		//3-遍历
		while(strIndex < str.length() && matchIndex < match.length()){
			if(strChar[strIndex] == matchChar[matchIndex]){
				strIndex++;
				matchIndex++;
			}else if(next[matchIndex] == -1){
				strIndex++;
			}else{
				//match数组向前滑动
				matchIndex = next[matchIndex];
			}
		}
		
		return matchIndex == match.length() ? strIndex - matchIndex : -1;
	}
	
	/**
	 * @author Ethan
	 * @desc 获取字符串的next数组
	 */
	public int[] nextArr(char[] match){
		//1-异常参数检测
		if(match.length == 1){
			return new int[]{-1};
		}
		//2-初始化指标
		int[] next = new int[match.length];
		//初始化next的前两个元素
		next[0] = -1;
		next[1] = 0;
		
		//初始化index
		int pos = 2;
		int cn = 0;
		
		//3-遍历和跳跃
		while(pos < next.length){
			if(match[pos] == match[cn]){
				next[pos++] = ++cn;
			}else if(cn > 0){
				//向前跳跃
				cn = next[cn];
			}else{
				next[pos++] = 0;
			}
		}
		return next;
	}
}
```
