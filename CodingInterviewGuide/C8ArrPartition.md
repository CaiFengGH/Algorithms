```
package Chapter8;

/**
 * @author Ethan
 * @desc 数组的partition调整 
 */
public class C8ArrPartition {

	/**
	 * @author Ethan
	 * @desc 已排序数组中左侧有序，右侧无序
	 * 1,2,2,2,3,3,4,5,6,6,7
	 * 1,2,3,4,5,6,7,...
	 */
	public void leftUnique(int[] num){
		//1-异常参数检测
		if(num == null || num.length == 0){
			return;
		}
		//2-初始化 A B两个区域边界
		int left = 0;
		int right = 1;
		//3-遍历交换
		while(right != num.length){
			if(num[right++] != num[left]){
				swap(num,++left,right - 1);
			}
		}
	}

	/**
	 * @author Ethan
	 * @desc 仅有0 1 2元素的排序
	 */
	public void sort(int[] num){
		//1-异常参数检测
		if(num == null || num.length == 0){
			return;
		}
		//2-初始化左中右分区 left: index: right
		int left = -1;
		int index = 0;
		int right = num.length;
		//3-遍历排序
		while(index < right){
			if(num[index] == 0){
				swap(num,++left,index++);
			}else if(num[index] == 2){
				swap(num,index,--right);
			}else{
				index++;
			}
		}
	}
	
	/**
	 * @author Ethan
	 * @desc 交换数组中的两个元素
	 */
	private void swap(int[] num, int i, int j) {
		int tmp = num[i];
		num[i] = num[j];
		num[j] = tmp;
	}
	
	public void printArr(int[] num){
		for(int i : num){
			System.out.println(i);
		}
	}
	
	public static void main(String[] args) {
		C8ArrPartition ap = new C8ArrPartition();
		int[] num = {1,2,2,2,3,3,4,5,6,6,7};

		System.out.println("开始调整前：");
		ap.printArr(num);

		ap.leftUnique(num);
		
		System.out.println("开始调整后：");
		ap.printArr(num);
		
		int[] num1 = {0,1,2,2,1,0};
		System.out.println("开始调整前：");
		ap.printArr(num1);
		
		System.out.println("开始调整后：");
		ap.sort(num1);
		ap.printArr(num1);
	}
}
```
