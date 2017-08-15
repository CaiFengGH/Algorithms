>桶排序

- 排序原理

确定待排序数组a的最大值max，生成元素个数为(max+1)的桶bucket，并初始化为0；

遍历数组a，读取每个a数组元素并将其值作为bucket的索引index,bucket[index]值加1，遍历到重复的值，重复加1；

最后从bucket中提取元素，生成已排序数组；

```
/**
 * @author Ethan
 * @desc 实现桶排序
 * @date 2017年8月15日
 */
public class BucketSort {
	
	/**
	 * @desc 桶排序
	 * @param arr 数组
	 * @param max 数组中最大值+1
	 */
	public void bucketSort(int[] arr,int max){
		//非法值传入
		if(arr == null || max < 1){
			return;
		}
		//初始化桶
		int[] bucket = new int[max];
		//遍历arr为桶中元素赋值
		for(int i = 0; i < arr.length; i++){
			bucket[arr[i]]++; 
		}
		//实现排序功能
		for(int i = 0,j = 0; i < max; i++){
			while((bucket[i]--) > 0){
				//桶中元素的索引就是arr中元素
				arr[j++] = i;
			}
		}
	}
}

```

[图片详解](http://images.cnitblog.com/i/497634/201403/152240225909832.jpg)
