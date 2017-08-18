>双端链表

- 注意事项

链表在头部和尾部插入和删除的时间复杂度为O(1)，在指定位置插入和删除时间复杂度为O(N);

链表的大小不受限制，不会因为数组大小固定；

```
/**
 * @author Ethan
 * @desc 实现双端链表 注:仅有一个节点时，头尾节点一致
 */
public class DoublyLinkedList {
	private ListNode first;
	private ListNode last;
	private int numItems;
	
	public DoublyLinkedList(){
		this.numItems = 0;
	}
	/**
	 * @desc 返回链表大小
	 * @return 返回大小值
	 */
	public int size(){
		return numItems;
	}
	/**
	 * @desc 链表是否为空
	 * @return 返回是否为空
	 */
	private boolean isEmpty() {
		return numItems == 0;
	}
	/**
	 * @desc 头插法
	 * @param value 插入值
	 */
	public void insertFirst(int value){
		ListNode newNode = new ListNode(value);
		//根据链表是否为空进行操作
		if(isEmpty()){
			last = newNode;
		}else{
			first.previous = newNode;
			newNode.next = first;
		}
		first = newNode;
		//链表数量增加
		numItems++;
	}
	/**
	 * @desc 尾插法
	 * @param value 插入值
	 */
	public void insertLast(int value){
		ListNode newNode = new ListNode(value);
		//根据链表是否为空进行处理
		if(isEmpty()){
			first = newNode;
		}else{
			last.next = newNode;
			newNode.previous = last;
		}
		last = newNode;
		numItems++;
	}
	/**
	 * @desc 在指定元素后面插入 
	 * @param key 指定值
	 * @param value 插入值
	 * @return 返回是否成功插入
	 */
	public boolean insertAfter(int key,int value){
		//寻找key所在的节点
		ListNode current = first;
		while(current != null){
			if(current.value == key){
				break;
			}
			current = current.next;
		}
		if(current == null){
			return false;
		}
		//如果current为尾节点
		if(current == last){
			insertLast(value);
		}else{
			ListNode newNode = new ListNode(value);
			current.next.previous = newNode;
			newNode.next = current.next;
			current.next = newNode;
			newNode.previous = current;
			numItems++;
		}
		return true;
	}
	/**
	 * @desc 删除头节点
	 * @return 返回删除
	 */
	public ListNode deleteFirst(){
		//链表为空
		if (first == null) {
			System.out.println("链表为空，不能删除头节点");
			return null;
		}	
		//仅有一个节点
		ListNode temp = first;
		if(first.next == null){
			first = null;
			last = null;
		}else{
			first.next.previous = null;
			first = first.next;
		}
		numItems--;
		return temp;
	}
	/**
	 * @desc 删除尾节点
	 * @return 返回删除尾节点
	 */
	public ListNode deleteLast(){
		//链表为空
		if (last == null) {
			System.out.println("链表为空，不能删除头节点");
			return null;
		}	
		//仅有一个节点
		ListNode temp = last;
		if(last.previous == null){
			first = null;
			last = null;
		}else{
			first.previous.next = null;
			last = last.previous;
		}
		numItems--;
		return temp;
	}
	/**
	 * @desc 删除指定节点
	 * @param key 指定节点值
	 * @return 返回删除节点
	 */
	public ListNode deleteAfter(int key){
		ListNode current = first;
		//寻找关键节点
		while(current != null){
			if(current.value == key){
				break;
			}
			current = current.next;
		}
		if(current == null){
			System.out.println("数组中无该值");
			return null;
		}
		if(current == last){
			return deleteLast();
		}
		current.previous.next = current.next;
		current.next.previous = current.previous;
		
		numItems--;
		return current;
	}
	/**
	 * @desc 从头到尾遍历链表 
	 */
	public void displayForward(){
		System.out.println("从头到尾遍历链表");
		ListNode current = first;
		while(current != null){
			System.out.print(current.value+"->");
			current = current.next;
		}
		System.out.println();
	}
	/**
	 * @desc 从尾到头遍历链表
	 */
	public void displayBackward(){
		System.out.println("从尾到头遍历链表");
		ListNode current = last;
		while(current != null){
			System.out.print(current.value+"->");
			current = current.previous;
		}
		System.out.println();
	}
}
/**
 * @author Ethan
 * @desc 链表节点
 */
class ListNode{
	public int value;
	public ListNode previous;
	public ListNode next;
	
	public ListNode(int value){
		this.value = value;
	}
}
```
