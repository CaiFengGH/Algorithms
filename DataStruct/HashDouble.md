>哈希表之再哈希化

- 定义

哈希表，通过哈希函数将关键字散列为存储地址，插入和删除操作均为O(1)，但是存在问题，如果不同的关键字散列为相同的存储地址？

- 再哈希化

不同的关键字散列为相同的存储地址，可以使用线性探测方法，依次寻找空白单元，易出现聚集现象；

二次探测，每次探测步长为平方级，可以解决聚集现象，易产生二次聚集；

再哈希化，首次哈希确定散列地址，发生冲突时再哈希确定探测步长；

- 注意事项

查找、增加及删除的时间复杂度均为O(1)，发生冲突时，时间复杂度由冲突解决方案有关，但最坏情况为O(N)；

```
/**
 * @author Ethan
 * @desc 基于再哈希的哈希表
 */
public class HashDouble {
	//哈希数组、数组大小、存储元素个数、删除表示
	private Item[] hashArr;
	private int arrSize;
	private int itemNum;
	private Item delItem;
	
	public HashDouble(){
		arrSize = 13;
		hashArr = new Item[arrSize];
		delItem = new Item(-1);
	}
	/**
	 * @desc 哈希表添加
	 */
	public void insert(Item item){
		//是否需要进行哈希表扩展
		if(isFull()){
			System.out.println("哈希表已满，重新哈希化");
			extendHashTable();
		}
		//获取元素的键
		int key = item.getKey();
		//计算两个哈希函数值
		int hashVal = hash1(key);
		int step = hash2(key);
		//进行插入
		while(hashArr[hashVal] != null && hashArr[hashVal].getKey() != -1){
			hashVal += step;
			hashVal = hashVal % arrSize;
		}
		hashArr[hashVal] = item;
		itemNum++;
	}
	/**
	 * @desc 哈希表查找
	 */
	public Item search(int key){
		int hashVal = hash1(key);
		int step = hash2(key);
		//寻找元素
		while(hashArr[hashVal] != null){
			if(hashArr[hashVal].getKey() == key){
				return hashArr[hashVal];
			}
			hashVal += step;
			hashVal = hashVal % arrSize;
		}
		return null;
	}
	/**
	 * @desc 哈希表删除
	 */
	public Item delete(int key){
		if(isEmpty()){
			System.out.println("哈希表为空，不能删除");
			return null;
		}
		int hashVal = hash1(key);
		int step = hash2(key);
		while(hashArr[hashVal] != null){
			if(hashArr[hashVal].getKey() == key){
				Item temp = hashArr[hashVal];
				hashArr[hashVal] = delItem;
				itemNum--;
				return temp;
			}
			hashVal += step;
			hashVal = hashVal % arrSize;
		}
		return null;
	}
	/**
	 * @desc 扩展哈希表
	 */
	public void extendHashTable(){
		int num = itemNum;
		itemNum = 0;
		arrSize = arrSize * 2;
		Item[] oldArr = hashArr;
		hashArr = new Item[arrSize];
		for(int i = 0; i < num ; i++){
			insert(oldArr[i]);
		}
	}
	/**
	 * @desc 哈希函数，用于索引
	 */
	public int hash1(int key){
		return key % arrSize;
	}
	/**
	 * @desc 哈希函数，用于再哈希化，确定探索步长
	 */
	public int hash2(int key){
		//常量 - key % 常量 其中：常量为不大于数组长度的质数
		return 7 - key % 7;
	}
	/**
	 * @desc 判断是否已满，用于扩展哈希表
	 */
	public boolean isFull(){
		return itemNum == arrSize;
	}
	/**
	 * @desc 判断是否为空，删除时方便 
	 */
	public boolean isEmpty(){
		return itemNum == 0;
	}
	
}
/**
 * @author Ethan
 * @desc 哈希表中存储元素
 */
class Item{
	private int data;
	public Item(int data){
		this.data = data;
	}
	/**
	 * @desc 获取元素键 
	 */
	public int getKey(){
		return data;
	}
}

```
