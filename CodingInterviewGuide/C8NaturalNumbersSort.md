```
package Chapter8;

/**
 * @author Ethan
 * @desc 实现自然数排序，即arr[i] = i + 1 
 * 时间复杂度为O(N)，空间复杂度为O(1)
 */
public class C8NaturalNumbersSort {

	/**
	 * @author Ethan
	 * @desc 基于跳跃的方式 
	 */
	public void naturalNumbersSort1(int[] arr){
		//1-异常参数检测
		if(arr == null || arr.length == 1){
			return ;
		}
		//2-初始化
		int tmp = 0;
		int next = 0;

		//3-循环跳跃
		for(int i = 0; i != arr.length; i++){
			tmp = arr[i];
			while(arr[i] != i + 1){
				next = arr[tmp - 1];
				arr[tmp - 1] = tmp;
				tmp = next;
			}
		}
	}
	
	/**
	 * @author Ethan
	 * @desc 基于交换的方式
	 */
	public void naturalNumbersSort2(int[] arr){
		//1-异常参数检测
		if(arr == null || arr.length == 1){
			return ;
		}
		//2-初始化
		int tmp = 0;
		//3-循环交换
		for(int i = 0; i != arr.length; i++){
			while(arr[i] != i + 1){
				tmp = arr[arr[i] - 1];
				arr[arr[i] - 1] = arr[i];
				arr[i] = tmp;
			}
		}
	}
}
```
