```
package Chapter5;

/**
 * @author Ethan
 * @desc 返回包含str2字符的str1子串的最小长度 
 */
public class C5MinLength {

	/**
	 * @author Ethan
	 * @desc 具体思路参考 
	 */
	public int minLength(String str1,String str2){
		//1-异常参数检测
		if(str1 == null || str2 == null || str1.length() < str2.length()){
			return 0;
		}
		//2-初始化 map
		char[] chas1 = str1.toCharArray();
		char[] chas2 = str2.toCharArray();
		int[] map = new int[256];
		for(int i = 0; i != str2.length();i++){
			map[chas2[i]]++;
		}
		//3-初始化四个变量  left: right: match: minLen:
		int left = 0;
		int right = 0;
		int match = chas2.length;
		int minLen = Integer.MAX_VALUE;
		
		//4-遍历
		while(right != chas1.length){
			//right向右伸展
			map[chas1[right]]--;
			if(map[chas1[right]] >= 0){
				match--;
			}
			
			if(match == 0){
				//left向左压缩
				while(map[chas1[left]] < 0){
					map[chas1[left++]]++;
				}
				minLen = Math.min(minLen, right - left + 1);
				match++;
				map[chas1[left++]]++;
			}
			right++;
		}
		
		return minLen = minLen == Integer.MAX_VALUE ? 0 : minLen;
	}
	
	public static void main(String[] args) {
		C5MinLength ml = new C5MinLength();
		String str1 = "adabbca";
		String str2 = "acb";
		
		int res = ml.minLength(str1, str2);
		System.out.println(res);
	}
}
```
