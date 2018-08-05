>堆排序

最大堆实现升序排序，最小堆实现降序排序；

- 实现方法

（1）将无序数组转换为最大堆；

（2）arr[0]与arr[n-1]交换，则arr[n-1]为最大值，继而实现0到n-2的最大堆顺序；继续进行交换，知道arr[0]与arr[1]交换，实现有序后，则完成最大堆的升序排序；

```
/**
 * @author Ethan
 * @desc 最大堆实现升序排序，最小堆实现降序排序
 */
public class HeapSort {
	
	/**
	 * @desc 堆排序
	 * @param arr 数组
	 * @param len 数组长度
	 */
	public void heapSortAsc(int[] arr,int len){
		//将二叉堆转换为最大堆
		for(int i = (len / 2) - 1; i >= 0; i--){
			maxHeapDown(arr,i,len - 1);
		}
		//循环交换元素实现升序排列
		int temp = 0;
		for(int j = len - 1; j > 0; j--){
			//将最大元素与末尾元素交换
			temp = arr[0];
			arr[0] = arr[j];
			arr[j] = temp;
			//保证0到j-1的最大堆排序
			maxHeapDown(arr,0,j - 1);
		}
	}
	/**
	 * @desc 最大堆向下
	 * @param arr 数组
	 * @param start 开始位置
	 * @param end 结束位置
	 */
	private void maxHeapDown(int[] arr, int start, int end) {
		//初始化当前节点索引+父节点索引
		int current = start;
		int leftChild = current * 2 + 1;
		int temp = 0;
		
		while(leftChild <= end){
			temp = arr[current];
			//比较左右子节点大小
			if(leftChild < end && arr[leftChild] < arr[leftChild+1]){
				leftChild++;
			}
			//比较当前值与子节点较大值
			if(temp > arr[leftChild]){
				break;
			}else{
				//交换当前节点和父节点的位置
				arr[current] = arr[leftChild];
				arr[leftChild] = temp;
				//更新当前节点和左子节点索引
				current = leftChild;
				leftChild = current * 2 + 1;  
			}
		}
	}
	/**
	 * @desc 打印堆的数组序列
	 * @param arr
	 */
	public void showHeap(int[] arr){
		System.out.println("数组为：");
		for(int i : arr){
			System.out.println(i+" ");
		}
	}
	/**
	 * @desc 测试堆排序
	 */
	public static void main(String[] args) {
		HeapSort hs = new HeapSort();
		int[] arr = {10,20,30,40,50,60,70,80,90};
		hs.heapSortAsc(arr, arr.length);
		hs.showHeap(arr);
	}
}
```
