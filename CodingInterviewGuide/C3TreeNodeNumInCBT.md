```
package Chapter3;

/**
 * @author Ethan
 * @desc 统计完全二叉树的节点个数 
 */
public class C3TreeNodeNumInCBT {

	/**
	 * @author Ethan
	 * @desc 基于递归思路求解完全二叉树的节点个数
	 */
	public int nodeNum(TreeNode head){
		//1-异常参数检测
		if(head == null){
			return 0;
		}
		//2-基于递归求解节点个数 
		return bs(head,1,mostLeftHeight(head,1));
	}

	/**
	 * @author Ethan
	 * @desc 结合完全二叉树的性质，统计二叉树的节点
	 * node:当前节点 l:当前节点的层数 h:树的高度
	 */
	private int bs(TreeNode node, int l, int h) {
		if(l == h){
			return 1;
		}
		//根据左子树
		if(mostLeftHeight(node.right,l + 1) == h){
			return 1 << (h - 1) + bs(node.right,l+1,h);
		}else{
			return 1 << (h - l - 1) + bs(node.left,l+1,h);
		}
	}

	/**
	 * @author Ethan
	 * @desc 一棵树的高度
	 */
	private int mostLeftHeight(TreeNode node, int level) {
		while(node != null){
			level++;
			node = node.left;
		}
		return level - 1;
	}
}

```
