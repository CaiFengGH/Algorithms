```
package Chapter8;

import java.util.Scanner;

/**
 * @author Ethan
 * @desc 获取数组中某一局部最小值的索引 
 */
public class C8GetLocalLeastIndex {

	public int localLeastIndex(int[] m){
		//1-异常参数检测
		//m为null或者长度为0
		if(m == null || m.length == 0){
			return -1;
		}
		//m长度为1，或者m[0]小于m[1]
		if(m.length == 1 || m[0] < m[1]){
			return 0;
		}
		//m[n-1]小于m[n-2]
		int len = m.length;
		if(m[len - 1] < m[len - 2]){
			return len - 1;
		}
		//2-二分查找搜索
		//初始化左右 left: right:
		int left = 1;
		int right = len - 2;
		int mid = 0;
		//二分搜索实现
		while(left < right){
			mid = (left + right) / 2;
			if(m[mid] > m[mid - 1]){
				right = mid - 1;
			}else if(m[mid] > m[mid + 1]){
				left = mid + 1;
			}else{
				return mid;
			}
		}
		return left;
	}
	
	public static void main(String[] args) {
		C8GetLocalLeastIndex li = new C8GetLocalLeastIndex();
		
		Scanner scan = new Scanner(System.in);
		String[] strArr = scan.nextLine().split(" ");
		int[] m = new int[strArr.length];
		
		for(int i = 0; i < strArr.length; i++){
			m[i] =Integer.valueOf(strArr[i]);
		}	
	
		int leastIndex = li.localLeastIndex(m);
		System.out.println(leastIndex);
	}
}
```
