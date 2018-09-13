```
package Chapter3;

import java.util.LinkedList;
import java.util.Queue;

/**
 * @author Ethan
 * @desc 是否是二叉搜索树或者是完全二叉树 
 */
public class C3IsTree {

	/**
	 * @author Ethan
	 * @desc 是否是二叉搜索树
	 */
	public boolean isBST(TreeNode head){
		if(head == null){
			return false;
		}
		//2-初始化 cur1: cur2:
		boolean res = true;
		TreeNode pre = null;
		TreeNode cur1 = head;
		TreeNode cur2 = null;
		
		//3-morris算法的过程
		while(cur1 != null){
			cur2 = cur1.left;
			if(cur2 != null){
				while(cur2.right != null && cur2.right != cur1){
					cur2 = cur2.right;
				}
				
				if(cur2.right == null){
					cur2.right = cur1;
					cur1 = cur1.left;
					continue;
				}else{
					cur2.right = null;
				}
			}
			if(pre != null && pre.value > cur1.value){
				return false;
			}
			pre = cur1;
			cur1 = cur1.right;
		}
		return res;
	}
	
	/**
	 * @author Ethan
	 * @desc 是否是完全二叉树
	 */
	public boolean isCBT(TreeNode head){
		//1-异常参数检测
		if(head == null){
			return false;
		}
		
		//2-初始化 queue: left: right: left:
		Queue<TreeNode> queue = new LinkedList<TreeNode>();
		queue.offer(head);
		TreeNode cur = null;
		TreeNode left = null;
		TreeNode right = null;
		boolean leaf = false;
		
		//3-队列出队入队
		while(!queue.isEmpty()){
			cur = queue.poll();
			left = cur.left;
			right = cur.right;
			
			//left为null，right不为null
			//left不为null，right为null，则后序节点均为叶子结点
			if((left == null && right != null) || 
					(leaf && (left != null || right != null)) ){
				return false;
			}
			
			if(left != null){
				queue.offer(left);
			}
			if(right != null){
				queue.offer(right);
			}else{
				leaf = true;
			}
		}
		return true;
	}
}
```
