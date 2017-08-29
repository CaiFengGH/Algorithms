>哈希表之链表

- 链表地址法

哈希表之再哈希为开放地址法，链表地址法与其相比，无需扩展哈希表，同时使用更加简便；

```
/**
 * @author Ethan
 * @desc 哈希表之链表
 */
public class HashChain{
	private SortedList[] hashArr;
	private int arrSize;
	
	public HashChain(){
		this.arrSize = 13;
		hashArr = new SortedList[arrSize];
		initArr();
	}
	/**
	 * @desc 实现哈希数组的初始化
	 */
	private void initArr() {
		for(int i = 0; i < arrSize; i++){
			hashArr[i] = new SortedList();
		}
	}
	/**
	 * @desc 计算哈希值
	 * @param key 关键字
	 */
	public int hash(int key){
		return key % arrSize;
	}
	/**
	 * @desc 哈希表的插入
	 * @param key 插入节点关键字
	 */
	public void insert(int key){
		int hashVal = hash(key);
		hashArr[hashVal].insert(key);
	}
	/**
	 * @desc 哈希表的删除
	 * @param key 删除节点的关键字
	 */
	public LinkedNode delete(int key){
		int hashVal = hash(key);
		LinkedNode temp = hashArr[hashVal].find(key);
		hashArr[hashVal].delete(key);
		return temp;
	}
	/**
	 * @desc 哈希表的插入
	 * @param key 查找节点的关键字
	 */
	public LinkedNode find(int key){
		int hashVal = hash(key);
		return hashArr[hashVal].find(key);
	}
}
/**
 * @author Ethan
 * @desc 有序链表 注:按照关键字升序排列
 */
class SortedList{
	//有序链表头节点
	private LinkedNode header;
	
	public SortedList(){
		
	}
	public SortedList(LinkedNode header){
		this.header = header;
	}
	
	/**
	 * @desc 有序链表的升序插入 
	 * @param key 插入节点关键字
	 */
	public void insert(int key){
		//初始化节点
		LinkedNode newNode = new LinkedNode(key);
		//初始化当前节点和前节点
		LinkedNode previous = null;
		LinkedNode current = header;
		//循环查找节点插入位置
		while(current != null && current.getKey() <= key){
			previous = current;
			current = current.next;
		}
		//插入头部
		if(previous == null){
			header = newNode;
		}else{
			previous.next = newNode;
			//包含中间插入和尾部插入
			newNode.next = current;
		}
	}
	/**
	 * @desc 有序链表的删除
	 * @param key 删除节点的关键字
	 */
	public void delete(int key){
		if(isEmpty()){
			return;
		}
		LinkedNode previous = null;
		LinkedNode current = header;
		while(current != null){
			if(current.getKey() == key){
				break;
			}
			previous = current;
			current = current.next;
		}
		if(current == null){
			return;
		}else{
			if(previous == null){
				header = current.next;
			}else{
				previous.next = current.next; 
			}
		}
	}
	/**
	 * @desc 有序链表的查找
	 * @param key 查找节点的关键字
	 * @return 返回关键字节点
	 */
	public LinkedNode find(int key){
		//初始化当前节点
		LinkedNode current = header;
		//循环查找节点
		while(current != null){
			if(current.getKey() == key ){
				return current;
			}
			current = current.next;
		}
		return null;
	}
	/**
	 * @desc 打印有序链表
	 */
	public void show(){
		System.out.println("有序链表如下");
		LinkedNode current = header;
		while(current != null){
			System.out.print(current.getKey()+"->");
			current = current.next;
		}
		System.out.print("null");
		System.out.println();
	}
	/**
	 * @desc 返回链表是否为空
	 */
	private boolean isEmpty() {
		return header == null;
	}
}
/**
 * @author Ethan
 * @desc 有序链表节点
 */
class LinkedNode{
	private int key;
	public LinkedNode next;
	public LinkedNode(int key){
		this.key = key;
	}
	public int getKey(){
		return this.key;
	}
}

```
