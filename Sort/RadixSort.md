>题目描述

基数排序

- 实现方法

寻找数组中最大值，确定其位数，假如只有三位；

一次对数组中个位/十位/百位/进行排序，三次排序后结果即为最终排序；

每次排序时基于桶排序实现；

```
package DayCode;

/**
 * @author Ethan
 * @desc  
 */
public class RadixSort {

	/**
	 * @author Ethan
	 * @desc 基数排序
	 */
	public void radixSort(int[] nums){
		//1-初始化 exp:指数 max:最大值
		int exp = 0;
		int len = nums.length;
		int max = getMax(nums,len);
		
		//2-连续排序
		for(exp = 1; max / exp > 0; exp *= 10){
			countSort(nums,exp,len);
		}
	}

	/**
	 * @author Ethan
	 * @desc 基于桶排序操作
	 */
	private void countSort(int[] nums, int exp, int len) {
		//1-初始化 tmp:中间数组 bucket:桶数组
		int[] tmp = new int[len];
		int[] bucket = new int[10];
		
		//2-基于个位/十位/百位/创建数组
		for(int i = 0; i < len; i++){
			bucket[(nums[i] / exp) % 10] += 1; 
		}
		
		//3-bucket[index] += bucket[index-1] : 此时记录的是在tmp中位置
		for(int j = 1; j < 10; j++){
			bucket[j] += bucket[j-1];
		}
		
		//4-初始化tmp
		for(int k = 0; k < len; k++){
			tmp[bucket[(nums[i] / exp) % 10] - 1] = nums[k];
			bucket[(nums[i] / exp) % 10]--;
		}
		
		//5-重新初始化nums
		for(int n = 0; n < len; n++){
			nums[n] = tmp[n];
		}
	}

	/**
	 * @author Ethan
	 * @desc 获取数组最大值
	 */
	private int getMax(int[] nums,int len) {
		int max = nums[0];
		
		for(int i = 1; i < len; i++){
			if(nums[i] > max){
				max = nums[i];
			}
		}
		return max;
	}

	public static void main(String[] args) {
		RadixSort rs = new RadixSort();
		int[] nums = {1,3,2,4,6,5};
		rs.radixSort(nums);
		for(Integer i: nums){
			System.out.println(i);
		}
	}
}

```

[基数排序](https://images0.cnblogs.com/i/497634/201403/161837176365265.jpg)
