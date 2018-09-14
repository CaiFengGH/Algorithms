```
package Chapter5;

/**
 * @author Ethan
 * @desc 返回数组中两个字符串出现的最短距离 
 */
public class C5MinDistance {

	/**
	 * @author Ethan
	 * @desc 返回最短距离 
	 */
	public int minDistance(String[] strArr,String str1,String str2){
		//1-异常参数检测
		if(strArr == null || strArr.length == 0){
			return -1;
		}
		if(str1 == null || str2 == null){
			return -1;
		}
		if(str1.equals(str2)){
			return 0;
		}
		
		//2-初始化 last1:str1最新出现的位置 last2:str2最新出现的位置 min:当前的最小距离
		int last1 = -1;
		int last2 = -1;
		int min = Integer.MAX_VALUE;
		
		//3-遍历，确定字符串最新出现的位置和最短距离
		for(int i = 0; i < strArr.length; i++){
			if(strArr[i].equals(str1)){
				min = Math.min(min, last2 == -1 ? min : i - last2);
				last1 = i;
			}
			if(strArr[i].equals(str2)){
				min = Math.min(min, last1 == -1 ? min : i - last1);
				last2 = i;
			}
		}
		return min = min == Integer.MAX_VALUE ? -1 : min;
	}
	
	public static void main(String[] args) {
		C5MinDistance c5 = new C5MinDistance();
		String[] strArr = {"1","3","3","3","2","3","1"};
		String str1 = "1";
		String str2 = "2";

		int res = c5.minDistance(strArr, str1, str2);
		System.out.println(res);
	}
}
```
