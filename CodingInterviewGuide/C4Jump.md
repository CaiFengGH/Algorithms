>题目描述

给定数组arr，arr[i] == k，代表从i位置向右移动1~k步，返回最少几步可以跳跃到数组末尾位置；

- 实现方法

初始化jump/cur/next，分别代表步数/当前步数最远距离/下一步最远距离

```
package Chapter4;

/**
 * @author Ethan
 * @desc 跳跃游戏
 */
public class C4Jump {
	
	public int jump(int[] arr){
		//1-异常参数检测
		if(arr == null || arr.length == 0){
			return 0;
		}
		//2-初始化 jump:跳跃步数 cur:当前步数最大值 next:下一步最大值
		int jump = 0;
		int cur = 0;
		int next = 0;
		
		//3-遍历移动
		for(int i = 0; i < arr.length; i++){
			if(cur < i){
				jump++;
				cur = next;
			}
			//每一步更新
			next = Math.max(next, i + arr[i]);
		}
		return jump;
	}
}

```
