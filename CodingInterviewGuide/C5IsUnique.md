```
package Chapter5;

/**
 * @author Ethan
 * @desc 给定字符数组中，每个字符是否只出现一次 
 */
public class C5IsUnique {

	/**
	 * @author Ethan
	 * @desc 基于map数组实现
	 */
	public boolean isUnique(char[] chas){
		//1-异常参数检测
		if(chas == null || chas.length == 0){
			return false;
		}
		//2-初始化数组
		boolean[] map = new boolean[256];
		//3-遍历判断
		for(int i = 0; i < chas.length; i++){
			if(map[chas[i]]){
				return false;
			}
			map[chas[i]] = true;
		}
		return true;
	}
}
```
