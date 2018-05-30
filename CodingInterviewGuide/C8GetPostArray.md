```
package Chapter8;

import java.util.HashMap;

/**
 * @author Ethan
 * @desc 根据树的前序和中序数组生成后序数组 
 */
public class C8GetPostArray {

	/**
	 * @author Ethan
	 * @desc 返回后序数组
	 * pre[1-2-4-5-3-6-7] in[4-2-5-1-6-3-7] 
	 */
	public int[] getPostArray(int[] pre,int[] in){
		//1-异常参数检测
		if(pre == null || in == null){
			return null;
		}
		//2-初始化后序数组
		int len = pre.length;
		int[] post = new int[len];
		
		//3-初始化中序数组索引
		HashMap<Integer,Integer> map = new HashMap<Integer,Integer>();
		for(int i = 0; i < len; i++){
			map.put(in[i], i);
		}
		
		//4-实现后序数组赋值
		setPostIndex(pre,0,len - 1,in,0,len-1,post,len - 1,map);
		
		return post;
	}
	
	/**
	 * @author Ethan
	 * @desc 设置后序数组元素 
	 * pre[1-2-4-5-3-6-7] in[4-2-5-1-6-3-7] 
	 */
	public int setPostIndex(int[] pre,int pi,int pj,int[] in,int ii,int ij,
			int[] post,int postIndex,HashMap<Integer,Integer> map){
		//1-递归结束条件
		if(pi > pj){
			return postIndex;
		}
		//2-post数组赋值
		post[postIndex--] = pre[pi];
		//3-获取中序数组中头节点位置
		int i = map.get(pre[pi]);
		
		//4-后序遍历先填充右子树
		postIndex = setPostIndex(pre, pi - i + ij + 1, pj, in, i + 1, ij, post, postIndex, map);
		
		return setPostIndex(pre, pi + 1, pi + i - ii, in, ii, i - 1, post, postIndex, map);
	}
}
```
