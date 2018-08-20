```
package Chapter1;

import java.util.Deque;
import java.util.LinkedList;

/**
 * @author Ethan
 * @desc 滑动窗口最大值 
 */
public class C1MaxInWindow {
	
	/**
	 * @author Ethan
	 * @desc 数组滑动窗口最大值 
	 * num:[4,3,5,4,3,3,6,7]
	 * res:[5,5,5,4,6,7]
	 */
	public int[] getMaxInWindow(int[] num,int size){
		//1-异常参数检测
		if(num == null || size < 1 || num.length < size){
			return null;
		}
		//2-初始化 res:结果数组 ll:双端队列 index:res索引
		int[] res = new int[num.length - size + 1];
		Deque<Integer> ll = new LinkedList<Integer>();
		int index = 0;
		
		//3-窗口滑动
		for(int i = 0; i < num.length; i++){
			//找到第一个大于当前值的值
			while(!ll.isEmpty() && num[ll.peekLast()] <= num[i]){
				ll.pollLast();
			}
			//添加对队列尾部
			ll.offerLast(i);
			//窗口内清除过期值
			if(ll.peekFirst() == i - size){
				ll.pollFirst();
			}
			//判断是否可以输出
			if(i >= size - 1){
				res[index++] = num[ll.peekFirst()];
			}
		}
		return res;
	}
}
```
