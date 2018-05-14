>二叉树三种遍历方式非递归

```
package DayCode;

import java.util.Stack;

/**
 * @author Ethan
 * @desc https://blog.csdn.net/snow_7/article/details/51788172
 */
public class BinaryTreeIterator {

	/**
	 * @author Ethan
	 * @desc 二叉树的前序遍历
	 */
	public void preOrder(TreeNode root){
		//1-异常参数检测
		if(root == null){
			return;
		}
		//2-初始化 stack:遍历节点压栈
		Stack<TreeNode> stack = new Stack<TreeNode>();
		TreeNode p = root;
		//3-循环遍历
		while(!stack.empty() || p != null){
			//4-将当前节点及左节点全部压栈
			while(p != null){
				System.out.print(p.val + "-->");
				stack.push(p);
				p = p.left;
			}
			if(!stack.empty()){
				//5-将当前节点p出栈且将p更新为右节点
				p = stack.pop();
				p = p.right;
			}
		}
		System.out.println();
	}
	
	public void inOrder(TreeNode root){
		//1-异常参数检测
		if(root == null){
			return;
		}
		//2-初始化 stack:存储遍历元素
		Stack<TreeNode> stack = new Stack<>();
		TreeNode p = root;
		//3-循环遍历
		while(!stack.empty() || p != null){
			//4-将当前节点的左孩子不断压栈
			while(p != null){
				stack.push(p);
				p = p.left;
			}
			//5-将当前节点p出栈，打印值，并将其更新为p的右孩子
			if(!stack.empty()){
				p = stack.pop();
				System.out.print(p.val+"-->");
				p = p.right;
			}
		}
		System.out.println();
	}
	
	public void postOrder(TreeNode root){
		//1-异常参数检测
		if(root == null){
			return;
		}
		//2-初始化 stack:遍历访问
		Stack<TreeNode> stack = new Stack<TreeNode>();
		TreeNode pre = null;
		TreeNode cur = root;
		stack.push(cur);
		//3-循环访问
		while(!stack.empty()){
			cur = stack.peek();
			//4-叶子节点直接出栈，非叶子节点，pre非空，且pre为当前节点的左节点或者右节点
			if(cur.left == null && cur.right == null || 
					pre != null && (pre == cur.left || pre == cur.right))
			{
				System.out.print(cur.val + "-->");
				stack.pop();
				pre = cur;
			}else{
				//5-先压入当前节点，再压入右节点，再压入左节点，则出栈顺序是后序的
				if(cur.right != null){
					stack.push(cur.right);
				}
				if(cur.left != null){
					stack.push(cur.left);
				}
			}
		}
	}
}

```
