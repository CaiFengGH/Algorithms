```
package Chapter8;

/**
 * @author Ethan
 * @desc 获取节点的后继节点，后继节点指的是中序遍历后的下一个节点
 */
public class C8GetNextNode {
	
	public Node getNextNode(Node node){
		//1-节点为空
		if(node == null){
			return node;
		}
		//2-节点存在右子树，右子树的最左节点
		if(node.right != null){
			return getLeftNode(node.right);
		}
		//3-节点不存在右子树
		else{
			Node parent = node.parent;
			while(parent != null && parent.left != node){
				node = parent;
				parent = node.parent;
			}
			return parent;
		}
	}

	/**
	 * @author Ethan
	 * @desc 获取最左节点
	 */
	private Node getLeftNode(Node node) {
		while(node.left != null){
			node = node.left;
		}
		return node;
	}
	
	/**
	 * @author Ethan
	 * @desc
	 *     6
	 *   /   \
	 *  3     9
	 *   \
	 *    4  
	 */
	public static void main(String[] args) {
		Node node1 = new Node(6);
		Node node2 = new Node(3);
		Node node3 = new Node(9);
		Node node4 = new Node(4);
		
		node1.left = node2;
		node1.right = node3;
		node2.parent = node1;
		node2.right = node4;
		node4.parent = node2;
		node3.parent = node1;
		
		C8GetNextNode gnn = new C8GetNextNode();
		Node res = gnn.getNextNode(node1);
		if(res != null){
			System.out.println(res.val);
		}else{
			System.out.println("无后继节点");
		}
	}
}
class Node{
	public int val;
	public Node left;
	public Node right;
	public Node parent;
	
	public Node(int val){
		this.val = val;
	}
}
```
