>希尔排序

- 排序原理

将间距为gap(步长)的元素分为一组，每组进行直接插入排序；

然后减小gap的值，对新形成的组继续进行插入排序，直到gap为1为止，此时为直接插入排序；

- 注意事项

希尔排序的时间复杂度与gap的选取有关，gap=1时为直接插入排序；

希尔排序可以简单理解为在多次分组中，将较大的元素移动到后面，提高效率；

```
/**
 * @author Ethan
 * @desc 实现希尔排序
 * @date 2017年8月15日
 */
public class ShellSort {
	
	/**
	 * @desc 希尔排序，直接插入排序的改进版
	 * @param arr 数组
	 * @param len 数组长度
	 */
	public void shellSort(int[] arr,int len){
		//gap为分组，每次自除以2
		for(int gap = len / 2; gap > 0; gap /= 2){
			//每次均有gap个组实现直接插入排序
			for(int i = 0; i < gap; i++){
				//具体组的直接插入排序实现
				for(int j = i + gap; j < len; j += gap){
					//当且仅当所取值小于有序组最大元素时，进行数组移位交换
					if(arr[j] < arr[j - gap]){
						int temp = arr[j];
						int k = j - gap;
						//具体进行移位交换
						while(k >= 0 && arr[k] > temp){
							arr[k + gap] = arr[k];
							k -= gap;
						}
						//将所取值填充到合适位置
						arr[k + gap] = temp;
					}
				}
			}
		}
	}
}
```

[图片详解1](http://images.cnitblog.com/i/497634/201403/122325434993142.jpg)
[图片详解2](http://images.cnitblog.com/i/497634/201403/122326119003263.jpg)
[图片详解3](http://images.cnitblog.com/i/497634/201403/122327477476249.jpg)
