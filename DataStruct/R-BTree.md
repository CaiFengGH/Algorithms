>红黑树

- 定义

红黑树是一种特殊的二叉搜索树，其每个节点多一个属性表是红黑色；

- 特性

1、每个节点不是红色就是黑色；

2、根节点为黑色；

3、每个叶子节点，即指向为空的节点，为黑色；

4、如果一个节点是红色，则其子节点为黑色；

5、任意一条路径上面黑色节点数量不能为其他路径的两倍；

- 应用

存储有序数据，时间复杂度为O(lgN)，效率高；

Java中的TreeMap和TreeSet采取此结构，Linux中虚拟内存采取此结构；

- 注意事项

红黑树是一种相对平衡的二叉搜索树，在添加和删除时，易造成树不平衡，主要通过变色、左旋和右旋来改变结构，使其相对平衡；

具体分类参照[红黑树看完包懂](http://blog.csdn.net/eson_15/article/details/51144079)

```
/**
 * @author Ethan
 * @desc 红黑树
 */
public class RBTree {
	private RBTNode root;
	
	public RBTree(RBTNode root){
		this.root = root;
	}
	/**
	 * @desc 左旋
	 */
	public void leftRotate(RBTNode lrNode){
		//x y的初始化
		RBTNode x = lrNode;
		RBTNode y = x.rightChild;
		//y的左子节点设置为x的右子节点，y左子节点的父节点为x
		x.rightChild = y.leftChild;
		if(y.leftChild != null){
			y.leftChild.parent = x;
		}
		//x的父节点设置为y的父节点，将x的父节点的左或者右子节点设置为y
		y.parent = x.parent;
		if(x.parent == null){
			root = y;
		}else{
			//判断x为其父节点的何种节点
			if(x == x.parent.leftChild){
				x.parent.leftChild = y;
			}else{
				x.parent.rightChild = y;
			}
		}
		//将y的左子节点设置为x，x的父节点设置为y
		y.leftChild = x;
		x.parent = y;
	}
	
	/**
	 * @desc 右旋
	 */
	public void rightRotate(RBTNode rrNode){
		RBTNode x = rrNode;
		RBTNode y = x.leftChild;
		//y的右子节点设置为x的左子节点，y右子节点的父节点为x
		x.leftChild = y.rightChild;
		if(y.rightChild != null){
			y.rightChild.parent = x;
		}
		//x的父节点设置为y的父节点，将x的父节点的左或者右子节点设置为y
		y.parent = x.parent;
		if(x.parent == null){
			root = y;
		}else{
			if(x == x.parent.leftChild){
				x.parent.leftChild = y;
			}else{
				x.parent.rightChild = x;
			}
		}
		//将y的右子节点设置为x，x的父节点设置为y
		y.rightChild = x;
		x.parent = y;
	}
	
	/**
	 * @desc 前序遍历方式打印
	 * @param current 当前节点
	 */
	public void preOrderPrint(RBTNode current){
		if(current != null){
			System.out.println(current.value);
			preOrderPrint(current.leftChild);
			preOrderPrint(current.rightChild);
		}
	}
	/**
	 * @desc 测试 
	 *       10         10
	 *      /          /
	 *     6          8 
	 *    / \        / \
	 *   4   8      6   9
	 *      / \    / \
	 *     7   9  4   7
     *   ->左旋          <-右旋      
	 */
	public static void main(String[] args) {
		RBTNode one = new RBTNode(10);
		RBTNode two = new RBTNode(6);
		RBTNode three = new RBTNode(4);
		RBTNode four = new RBTNode(8);
		RBTNode five = new RBTNode(7);
		RBTNode six = new RBTNode(9);
		
		one.leftChild = two;
		two.leftChild = three;
		two.rightChild = four;
		four.leftChild = five;
		four.rightChild = six;
		two.parent = one;
		three.parent = two;
		four.parent = two;
		five.parent = four;
		six.parent = four;
		
		RBTree rbt = new RBTree(one);
		rbt.preOrderPrint(one);
		rbt.leftRotate(two);
		rbt.preOrderPrint(one);
		rbt.rightRotate(four);
		rbt.preOrderPrint(one);
	}
}
/**
 * @author Ethan
 * @desc 红黑树节点
 */
class RBTNode{
	public int value;
	public RBTNode leftChild;
	public RBTNode rightChild;
	public RBTNode parent;
	//黑:true 红:false
	public boolean isBlack = false;
	
	public RBTNode(int value){
		this.value = value;
	}
}
```
