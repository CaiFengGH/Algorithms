```
package Chapter8;

/**
 * @author Ethan
 * @desc 未排序正数数组累加和满足给定值的最大子数组的长度
 */
public class C8GetMaxLength {

	/**
	 * @author Ethan
	 * @desc  基于left和right滑动的方法
	 */
	public int getMaxLength(int[] arr,int k){
		//1-异常参数检测
		if(arr == null || arr.length == 0){
			return 0;
		}
		//2-初始化
		int left = 0;
		int right = 0;
		int sum = arr[0];
		int arrLen = arr.length;
		int len = 0;
		
		//3-left和right移动
		while(right < arrLen){
			if(sum == k){
				//更新最大值
				len = Math.max(len,right - left + 1);
				//left右移
				sum -= arr[left++];
			}else if(sum < k){
				right++;
				//此处无判断，会抛出NullPointerException
				if(right == arrLen){
					break;
				}
				sum += arr[right];
			}else{
				sum -= arr[left++];
			}
		}
		return len;
	}
}
```
