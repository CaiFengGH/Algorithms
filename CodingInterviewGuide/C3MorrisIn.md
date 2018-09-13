```
package Chapter3;

/**
 * @author Ethan
 * @desc 基于Morris的神级遍历方法 
 */
public class C3MorrisIn {
	
	/**
	 * @author Ethan
	 * @desc 基于Morris的中序遍历方法 
	 *       4
	 *     2   6 
	 *   1 3  5 7
	 */
	public void morrisIn(TreeNode head){
		//1-异常参数检测
		if(head == null){
			return;
		}
		//2-初始化 cur1: cur2:
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
			System.out.println(cur1.value);
			cur1 = cur1.right;
		}
		System.out.println();
	}
	
	public static void main(String[] args) {
		C3MorrisIn mi = new C3MorrisIn();
		
		TreeNode a = new TreeNode(4);
		TreeNode b = new TreeNode(2);
		TreeNode c = new TreeNode(6);
		TreeNode d = new TreeNode(1);
		TreeNode e = new TreeNode(3);
		
		a.left = b;
		a.right = c;
		
		b.left = d;
		b.right = e;
		
		mi.morrisIn(a);
	}
}
```
