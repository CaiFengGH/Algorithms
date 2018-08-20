```
package Chapter3;

/**
 * @author Ethan
 * @desc 返回最近的公共祖先 
 */
public class C3LowestAncestor {
	
	/**
	 * @author Ethan
	 * @desc 
	 */
	public TreeNode lowestAncestor(TreeNode head,TreeNode o1,TreeNode o2){
		if(head == null || head == o1 || head == o2){
			return head;
		}
		//1-左子树结果
		TreeNode left = lowestAncestor(head.left,o1,o2);
		//2-右子树结果
		TreeNode right = lowestAncestor(head.right,o1,o2);
		
		//3-左右子树结果均不为空
		if(left != null && right != null){
			return head;
		}
		return left != null ? left : right;
	}
}

```
