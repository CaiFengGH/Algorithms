```
package Basic;

/**
 * @author Ethan
 * @desc 中位数问题 
 */
public class Array_UpMedian {
	
	/**
	 * @author Ethan
	 * @desc 在两个等长的有序数组中返回上中位数
	 */
	public int getUpMedianInSameLength(int[] arr1,int[] arr2){
		//1-异常参数检测
		if(arr1 == null || arr2 == null || arr1.length != arr2.length){
			return -1;
		}
		//2-初始化
		int start1 = 0;
		int end1 = arr1.length - 1;
		int start2 = 0;
		int end2 = arr2.length - 1;
		int mid1 = 0;
		int mid2 = 0;
		int offset = 0;
		//3-循环更新
		while(start1 < end1){
			//更新mid1 mid2 offset
			mid1 = (start1 + end1) / 2;
			mid2 = (start2 + end2) / 2;
			//奇数：0 偶数：1 
			offset = ((end1 - start1 + 1) & 1) ^ 1; 
			
			if(arr1[mid1] > arr2[mid2]){
				end1 = mid1;
				start2 = mid2 + offset;
			}else if(arr1[mid1] < arr2[mid2]){
				start1 = mid1 + offset;
				end2 = mid2;
			}else{
				return arr1[mid1];
			}
		}
		return Math.min(arr1[start1], arr2[start2]);
	}
	
	public static void main(String[] args) {
		int[] arr1 = {1,2,3,4};
		int[] arr2 = {3,4,5,6};
		
		Array_UpMedian au = new Array_UpMedian();
		int res = au.getUpMedianInSameLength(arr1, arr2);
		System.out.println(res);
	}
}
```
