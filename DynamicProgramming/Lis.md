- 最长子序列

最长子序列的长度以及最长子序列的子序列；

链接：[动态规划之最长子序列](https://www.cnblogs.com/little-YTMM/p/5372680.html)

```
package DayCode;

import java.util.ArrayList;
import java.util.Collections;

/**
 * @author Ethan
 * @desc 最长递增子序列问题 
 */
public class Lis {

	/**
	 * @author Ethan
	 * @desc 最长子序列大小 
	 */
	public int numOfLis(int[] arr) {
		//1-异常参数检测
        if(arr == null || arr.length == 0)
            return 0;
        
        int[] b = new int[arr.length];
        b[0] = 1;
        int result = 1;
        
        for(int i = 1; i < arr.length; i++) {
            int max = -1;
            //2-寻找小于i的最大值，max不断被更新
            for(int j = 0; j < i; j++) {
                if(arr[j] < arr[i] && b[j] > max)
                    max = b[j];
            }
            b[i] = max + 1;
            result = Math.max(result, b[i]);
        }
        return result;
    }
	
	/**
	 * @author Ethan
	 * @desc 最长子序列的子序列
	 */
	public ArrayList<Integer> detailOfLis(int[] arr) {
		//1-异常参数检测
        if(arr == null || arr.length == 0)
            return null;
        //2- b为大小 b1为记录元素
        int[] b = new int[arr.length];
        int[] b1 = new int[arr.length];
        b[0] = 1;
        b1[0] = -1;
        
        //3-result:最大程度 index:最大长度的最后一个元素
        int result = 1;
        int index = 0;
        
        for(int i = 1; i < arr.length; i++) {
            int max = -1;
            boolean flag = false;
            
            for(int j = 0; j < i; j++) {
                if(arr[j] < arr[i] && b[j] > max) {
                    flag = true;
                    max = b[j];
                    b1[i] = j;
                }
            }
            if(flag == false) b1[i] = -1;
            b[i] = max + 1;
            if(result < b[i]) {
                result = b[i];
                index = i;
            }
        }
        ArrayList<Integer> res = new ArrayList<Integer>();
        for(;index >=0; ) {
            res.add(arr[index]);
            index = b1[index];
        }
        Collections.reverse(res);
        return res;
    }
	
	
	public static void main(String[] args) {
		Lis l = new Lis();
		int[] arr = {4,1,6,2,8,9,7};
		
		System.out.println(l.numOfLis(arr));
		
		ArrayList<Integer> al = l.detailOfLis(arr);
		
		for(int i : al){
			System.out.println(i+"--");
		}
	}
}

```
