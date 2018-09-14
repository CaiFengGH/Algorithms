```
package Chapter3;

/**
 * @author Ethan
 * @desc 判断数组是否是二叉树的后序遍历结果 
 */
public class C3IsPost {

	/**
	 * @author Ethan
	 * @desc  
	 */
	public boolean isPostArr(int[] nums){
		if(nums == null || nums.length == 0){
			return false;
		}
		return isPost(nums,0,nums.length - 1);
	}
	
	/**
	 * @author Ethan
	 * @desc 判断是否是 
	 */
	private boolean isPost(int[] nums,int start,int end) {
		//1-异常参数检测
		if(start == end){
			return true;
		}
		//2-初始化边界 less: more:
		int less = -1;
		int more = end;
		//3-遍历数组确定边界
		for(int i = start; i < end; i++){
			if(nums[end] > nums[i]){
				less = i;
			}else{
				more = more == end ? i : more;
			}
		}
		//4-less与more检测
		if(less == -1 || more == end){
			return isPost(nums,start,end - 1);
		}
		
		if(less != more - 1){
			return false;
		}
		return isPost(nums,start,less) && isPost(nums,more,end - 1);
	}
}
```
