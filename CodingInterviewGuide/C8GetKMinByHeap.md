```
package Chapter8;

/**
 * @author Ethan
 * @desc 通过最大堆获取无序数组中最小的k个值 
 */
public class C8GetKMinByHeap {

	/**
	 * @author Ethan
	 * @desc 利用堆的建堆和堆调整过程
	 */
	public int[] getKMinByHeap(int[] nums,int k){
		//1-异常参数检测
		if(nums == null || k < 1 || nums.length < k){
			return null;
		}
		//2-初始化最大堆
		int[] kHeap = new int[k];
		//3-建堆
		for(int i = 0; i < k; i++){
			heapInsert(kHeap,i,nums[i]);
		}
		
		//4-调整堆
		for(int i = k; i < nums.length; i++){
			if(nums[i] < kHeap[0]){
				kHeap[0] = nums[i];
				heapModify(kHeap,0,k-1);
			}
		}
		return kHeap;
	}

	/**
	 * @author Ethan
	 * @desc 最大堆调整 
	 */
	private void heapModify(int[] kHeap, int index, int end) {
		//1-初始化 left: largest:
		int left = 2 * index + 1;
		int parent = index;
		//2-从从往下调整
		while(left <= end){
			//比较左右子节点的最大值
			if(left < end && kHeap[left] < kHeap[left + 1]){
				left++;
			}
			//和parent比较
			if(kHeap[parent] < kHeap[left]){
				swap(kHeap,parent,left);
			}else{
				break;
			}
			parent = left;
			left = 2 * parent + 1;
		}
	}

	/**
	 * @author Ethan
	 * @desc 最大堆建堆 
	 */
	private void heapInsert(int[] kHeap,int index,int value) {
		//1-初始化
		kHeap[index] = value;
		int parent = 0;
		//2-调整
		while(index != 0){
			parent = (index - 1) / 2;
			if(kHeap[parent] < kHeap[index]){
				swap(kHeap,parent,index);
				index = parent;
			}else{
				break;
			}
		}
	}

	/**
	 * @author Ethan
	 * @desc 交换数组中的两个值
	 */
	private void swap(int[] nums, int i, int j) {
		int tmp = nums[j];
		nums[j] = nums[i];
		nums[i] = tmp;
	}
	
	public static void main(String[] args) {
		C8GetKMinByHeap gkbh = new C8GetKMinByHeap();
		int[] nums = {4,3,2,1,6,5,8};
		int[] res = gkbh.getKMinByHeap(nums, 3);
		for(int i : res){
			System.out.println(i);
		}
	}
}
```
