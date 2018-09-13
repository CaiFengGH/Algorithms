```
package Chapter3;

/**
 * @author Ethan
 * @desc 基于一个有序数组生成一个AVL树 
 */
public class C3GenerateAVLTree {

	/**
	 * @author Ethan
	 * @desc AVL:左右子树高度差最大为1
	 */
	public TreeNode generateAVL(int[] sortArr){
		//1-异常参数判断
		if(sortArr == null || sortArr.length == 0){
			return null;
		}
		//2-生成树
		return generateAVLTree(sortArr,0,sortArr.length - 1);
	}

	/**
	 * @author Ethan
	 * @desc 基于递归实现 
	 */
	private TreeNode generateAVLTree(int[] sortArr, int start, int end) {
		if(start > end){
			return null;
		}
		int mid = (start + end) / 2;
		TreeNode head = new TreeNode(sortArr[mid]);

		head.left = generateAVLTree(sortArr, start, mid - 1);
		head.right = generateAVLTree(sortArr, mid + 1, end);
		
		return head;
	}
}
```
