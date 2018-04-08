>快速选择

快速选择数组中第k小的数字；

- 实现方法

参考快速排序方法，找到第k小元素；

```
package DayCode;

/**
 * @author Ethan
 * @desc 实现快速选择，返回第k小的数，模仿快速排序思想 
 */
public class QuickSelect {

	public int quickSelect(int[] nums,int lo,int hi,int k){
		//1-初始化 i j init
		int i = lo;
		int j = hi;
		int init = nums[hi];
		
		//2-将大于init的值移动到右侧
		while(i < j){
			if(nums[i++] > init){
				swap(nums,--i,--j);
			}
		}
		swap(nums,i,hi);
		
		//判断前面还有多少个元素
		int m = i - lo + 1;
		 
		if(m == k){
			return i;
		}else if(m > k){
			return quickSelect(nums,lo,i-1,k);
		}else{
			return quickSelect(nums,i + 1,hi,k - m);
		}
		
	}

	private void swap(int[] nums, int i, int j) {
		int tmp = nums[i];
		nums[i] = nums[j];
		nums[j] = tmp;
	}
	
}

```
