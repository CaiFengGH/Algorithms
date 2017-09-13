>题目描述

找出指定数组中，和为定值的数字；

```
import java.util.HashMap;

public class Solution {
    public int[] twoSum(int[] nums, int target) {
    	int[] res = new int[2];
        //初始化hashMap，以值为键，以索引位置
        HashMap<Integer,Integer> map = new HashMap<Integer,Integer>();
        for(int i = 0; i < nums.length; i++){
            map.put(nums[i], i);
        }
        //循环遍历所有的值，搜索是否存在键
        for(int j = 0; j < nums.length; j++){
        	int temp = target - nums[j];
        	if(map.containsKey(temp) && map.get(temp) != j){
        		res[0] = j;
        		res[1] = map.get(temp);
        		break;
        	}
        }
        return res;
    }
    
    /**
     * @desc 测试two sum函数 
     */
    public static void main(String[] args) {
		int[] nums = {3,2,4};
		int target = 6;
		Solution s = new Solution();
		int[] res = s.twoSum(nums, target);
		System.out.println(res[0] + " " + res[1]);
	}
}
```
