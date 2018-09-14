```
package Chapter5;

/**
 * @author Ethan
 * @desc 在有序但含null的数组中寻找某个元素的位置 
 */
public class C5FindIndexInSortWithNull {

	/**
	 * @author Ethan
	 * @desc 基于二分搜索情况判断 
	 */
	public int getIndex(String[] strArr,String str){
		//1-异常参数检测
		if(strArr == null || strArr.length == 0 || str.length() == 0
				|| str == null){
			return -1;
		}
		//2-初始化 left: right: mid: res: i:
		int left = 0;
		int right = strArr.length - 1;
		int mid = 0;
		int res = -1;
		int index = 0;
		
		//3-二分搜索遍历
		while(left <= right){
			mid = (left + right) / 2;
			//4-mid非null，且相等
			if(strArr[mid] != null && strArr[mid].compareTo(str) == 0){
				res = mid;
				//最左位置
				right = mid - 1;
			}
			//5-mid非null，不等
			else if(strArr[mid] != null){
				if(strArr[mid].compareTo(str) < 0){
					left = mid + 1;
				}else{
					right = mid - 1;
				}
			}
			//6-mid为null
			else{
				index = mid;
				while(strArr[index] == null && --index >= left){}
				//左边全部为null 或者 第一个非空小
				if(index < left || strArr[index].compareTo(str) < 0){
					left = mid + 1;
				}else{
					res = strArr[index].compareTo(str) == 0 ? index : res;
					right = index - 1;
				}
			}
		}
		return res;
	}
	
	public static void main(String[] args) {
		C5FindIndexInSortWithNull c5 = new C5FindIndexInSortWithNull();
		String[] strArr = {null,"a","a",null,"b",null};
		String str = "c"; 
		
		int res = c5.getIndex(strArr, str);
		System.out.println(res);
	}
}

```
