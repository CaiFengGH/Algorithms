```
package Chapter5;

/**
 * @author Ethan
 * @desc 寻找在字符串中给定位置的新字符串 
 */
public class C5FindNewChar {

	/**
	 * @author Ethan
	 * @desc 返回k位置的新字符串 
	 */
	public String findNewChar(String str,int k){
		//1-异常参数检测
		if(str == null || str.length() == 0 || k < 0 || k >= str.length()){
			return null;
		}
		//2-初始化 chas: uNum:
		char[] chas = str.toCharArray();
		int uNum = 0;
		//3-寻找给定位置之前的大写字母数量
		for(int i = k - 1; i >= 0; i--){
			if(!Character.isUpperCase(chas[i])){
				break;
			}
			uNum++;
		}
		//4-分情况判断
		//uNum为奇数
		if((uNum & 1) == 1){
			return str.substring(k-1, k+1);
		}
		//k处为大写
		if(Character.isUpperCase(chas[k])){
			return str.substring(k,k+2);
		}
		return String.valueOf(chas[k]);
	} 
	
	public static void main(String[] args) {
		C5FindNewChar c5 = new C5FindNewChar();
		String str = "aaABCDEcBCg"; 
		String res = c5.findNewChar(str, 7);
		System.out.println(res);
	}
}

```
