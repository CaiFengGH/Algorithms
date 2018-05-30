```
package Chapter8;

/**
 * @author Ethan
 * @desc 返回数组中需要排序的最小长度 
 */
public class C8GetMinLength {

	/**
	 * @author Ethan
	 * @desc leftMinIndex rightMaxIndex
	 * 默认升序排序
	 * 从右往左确定最左最小值索引，从左往右确定最右最大值索引
	 */
	public int getMinLength(int[] num){
		//1-异常参数检测
		if(num == null || num.length < 2){
			return 0;
		}
		int len = num.length;
		//2-从右往左遍历
		int min = num[len - 1];
		int leftMinIndex = len - 1;
		
		for(int i = len - 2; i != -1; i--){
			//比最小值大则更新最左最小索引
			if(num[i] > min){
				leftMinIndex = i;
			}
			//否则更新最小值
			else{
				min = num[i];
			}
		}
		//3-从左往右遍历
		int max = num[0];
		int rightMaxIndex = 0;
		
		for(int i = 1; i != len; i++){
			//比最大值小则更新最右最大索引
			if(num[i] < max){
				rightMaxIndex = i;
			}
			//否则更新最大值
			else{
				max = num[i];
			}
		}

		//4-计算需要排序的最小长度
		return rightMaxIndex - leftMinIndex + 1;
	}
}

```
