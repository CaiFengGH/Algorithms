>二叉查找树常用方法

- 定义

一个节点的左子节点的关键值小于它，右子节点的关键值大于它；

- 常用方法

前序、中序及后序遍历，序以根节点为准，前则为根节点第一，左子节点次之，右子节点次之；

插入、寻找及最大值和最小值；

- 删除包括三种类型，叶子节点、一个子节点及两个子节点：

叶子节点删除，仅需要改变其父节点的左右关系；

一个子节点，仅需要改变其与父节点之间的关系；

两个子节点，重点在于寻找后继节点，包括右节点和最左节点两种类型；

```
/**
 * @author Ethan
 * @desc 二叉搜索树
 */
public class BinaryTree {
	private BTNode root;
	
	public BinaryTree(BTNode root){
		this.root = root;
	}
	
	/**
	 * @desc 
	 * @param id
	 * @param value
	 */
	public boolean insert(int id,int value){
		//根节点是否为空
		if(root == null){
			return false;
		}
		BTNode newNode = new BTNode(id,value);
		//按照二叉搜索树的顺序进行循环
		BTNode current = root;
		BTNode parent = null;
		while(true){
			parent = current;
			if(value < current.value){
				current = current.leftChild;
				//判断current是否为空
				if(current == null){
					parent.leftChild = newNode;
					newNode.parent = parent;
					return true;
				}
			}else if(value > current.value){
				current = current.rightChild;
				if(current == null){
					parent.rightChild = newNode;
					newNode.parent = parent;
					return true;
				}
			}else{
				return false;
			}
		}
	}
	/**
	 * @desc 搜索
	 * @param id 节点序号
	 * @return 返回节点
	 */
	public BTNode search(int value){
		BTNode current = root;
		//优先判断当前节点是否为空
		while(current != null && current.value != value){
			if(value < current.value){
				current = current.leftChild;
			}else{
				current = current.rightChild;
			}
		}
		return current;
	}
	/**
	 * @desc 最小值
	 * @return 返回最小键所在节点
	 */
	public BTNode min(){
		BTNode current = root;
		BTNode parent = null;
		while(current != null){
			parent = current;
			current = current.leftChild;
		}
		return parent;
	}
	/**
	 * @desc 最大值
	 * @return 返回最大键所在节点
	 */
	public BTNode max(){
		BTNode current = root;
		BTNode parent = null;
		while(current != null){
			parent = current;
			current = current.rightChild;
		}
		return parent;
	}
	/**
	 * @desc 遍历方式，打印节点的value值
	 */
	public void traverse(int selectNeed){
		switch(selectNeed){
		
		case 0: System.out.println("preOrder traverse");
				preOrder(root);
				break;
		
		case 1: System.out.println("inOrder traverse");
				inOrder(root);
				break;
		
		case 2: System.out.println("postOrder traverse");		
				postOrder(root);
				break;
				
		default: System.out.println("default traverse");
				inOrder(root);
		}
	}
	/**
	 * @desc 前序遍历 
	 */
	public void preOrder(BTNode localRoot){
		if(localRoot != null){
			System.out.println(localRoot.value);
			preOrder(localRoot.leftChild);
			preOrder(localRoot.rightChild);
		}
	}
	/**
	 * @desc 中序遍历
	 */
	public void inOrder(BTNode localRoot){
		if(localRoot != null){
			inOrder(localRoot.leftChild);
			System.out.println(localRoot.value);
			inOrder(localRoot.rightChild);
		}
	}
	/**
	 * @desc 后序遍历
	 */
	public void postOrder(BTNode localRoot){
		if(localRoot != null){
			postOrder(localRoot.leftChild);
			postOrder(localRoot.rightChild);
			System.out.println(localRoot.value);
		}
	}
	/**
	 * @desc 删除
	 * @param value
	 * @return 返回是否删除
	 */
	public boolean delete(int value){
		//找到待删除节点，并记录其为父节点的左右子树
		boolean isLeftChild = false;
		BTNode current = root;
		
		if(current == null){
			return false;
		}
		
		while(current.value != value){
			if(value < current.value){
				isLeftChild = true;
				current = current.leftChild;
			}else{
				isLeftChild = false;
				current = current.rightChild;
			}
			if(current == null){
				return false;
			}
		}
		//判断是叶节点 一个节点 和 两个节点的删除类型
		if(current.leftChild == null && current.rightChild == null){
			return deleteNoChild(current,isLeftChild);
		}else if(current.leftChild != null && current.rightChild != null){
			return deleteTwoChild(current,isLeftChild);
		}else{
			return deleteOneChild(current,isLeftChild);
		}
	}
	/**
	 * @desc 删除之叶节点
	 * @param node
	 * @param isLeftChild
	 */
	private boolean deleteNoChild(BTNode node, boolean isLeftChild) {
		//待删除节点为根节点
		if(node == root){
			root = null;
			return true;
		}
		if(isLeftChild){
			node.parent.leftChild = null;
		}else{
			node.parent.rightChild = null;
		}
		return true;
	}
	/**
	 * @desc 删除之一个子节点
	 */
	private boolean deleteOneChild(BTNode node, boolean isLeftChild) {
		//判断待删除节点的子节点方向
		if(node.leftChild == null){
			//待删除节点是否为根节点
			if(node == root){
				root = node.leftChild;
				node.parent = null;
				return true;
			}
			//待删除节点是其父节点的左子树还是右子树
			if(isLeftChild){
				node.parent.leftChild = node.rightChild;
			}else{
				node.parent.rightChild = node.rightChild;
			}
			node.rightChild.parent = node.parent;
		}else{
			//待删除节点是否为根节点
			if(node == root){
				root = node.leftChild;
				node.parent = null;
				return true;
			}
			//待删除节点是其父节点的左子树还是右子树
			if(isLeftChild){
				node.parent.leftChild = node.leftChild;
			}else{
				node.parent.rightChild = node.leftChild;
			}
			node.leftChild.parent = node.parent;
		}
		return true;
	}
	/**
	 * @desc 删除之两个子节点
	 */
	private boolean deleteTwoChild(BTNode node, boolean isLeftChild) {
		//寻找后继节点
		BTNode successor = getSuccessor(node);
		//判断后继节点是否为根节点
		if(node == root){
			successor.leftChild = root.leftChild;
			successor.parent = null;
			root = successor;
			
		}else{
			if(isLeftChild){
				node.parent.leftChild = successor;
			}else{
				node.parent.rightChild = successor;
			}
			successor.leftChild = node.leftChild;
		}
		return true;
	}
	/**
	 * @desc 获得待删除节点的后继节点，右节点或者最深左节点 
	 */
	private BTNode getSuccessor(BTNode node) {
		BTNode successor = node;
		//寻找后继节点
		BTNode current = node.rightChild;
		
		while(current != null){
			successor = current;
			current = current.leftChild;
		}
		//后继节点的两种类型
		if(successor != node.rightChild){
			//设置后继的父节点的左子节点
			successor.parent.leftChild = successor.rightChild;
			if(successor.rightChild != null){
				successor.rightChild.parent = successor.parent;
			}
			//设置后继的右子节点
			successor.rightChild = node.rightChild;
		}
		return successor;
	}

}
/**
 * @author Ethan
 * @desc 二叉树节点
 */
class BTNode{
	public int id;
	public int value;
	//父节点 左子节点 右子节点
	public BTNode parent;
	public BTNode leftChild;
	public BTNode rightChild;
	
	public BTNode(int id,int value){
		this.id = id;
		this.value = value;
	}
}
```
