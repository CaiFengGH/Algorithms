```
package Chapter3;

/**
 * @author Ethan
 * @desc 
 */
public class C3IsBalance {
	
	/**
	 * @author Ethan
	 * @desc 判断树是否是一个平衡树  
	 */
	public boolean isBalance(TreeNode root){
		boolean[] res = new boolean[1];
		//一个元素的数组类似于全局变量
		res[0] = true;
		getHeight(root,1,res);
		return res[0];
	}

	/**
	 * @author Ethan
	 * @desc 记录子树的高度，同时记录是否是平衡的
	 */
	private int getHeight(TreeNode head, int level, boolean[] res) {
		if(head == null){
			return level;
		}
		
		int leftHeight = getHeight(head.left,level + 1,res);
		if(!res[0]){
			return level;
		}
		int rightHeight = getHeight(head.right,level + 1,res);
		if(!res[0]){
			return level;
		}
		
		if(Math.abs(rightHeight - leftHeight) > 1 ){
			res[0] = false;
		}
		
		return Math.max(leftHeight, rightHeight);
	}
}

```
