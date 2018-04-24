>题目描述

实现字符串中句子逆序；实现旋转字符串；

- 实现方法

```
package Chapter5;

/**
 * @author Ethan
 * @desc 字符串反转系列 
 */
public class C5Rotate {

	/**
	 * @author Ethan
	 * @desc 反转句子中单词
	 */
	public void rotateWord(char[] cha){
		//1-异常参数判断
		if(cha == null || cha.length == 0){
			return ;
		}
		//2-第一次反转
		reverse(cha,0,cha.length - 1);
		//3-单词反转
		int left = -1;
		int right = -1;
		for(int i = 0; i < cha.length; i++){
			if(cha[i] != ' '){
				left = i == 0 || cha[i-1] == ' ' ? i : left;
				right = i == cha.length - 1 || cha[i+1] == ' ' ? i : right;
			}
			if(left != -1 && right != -1){
				reverse(cha,left,right);
				left = -1;
				right = -1;
			}
		}
	}

	/**
	 * @author Ethan
	 * @desc 将字符串左边m个元素移动到右边 
	 */
	public void rotate(char[] cha,int size){
		if(cha == null || cha.length == 0 || size <= 0 || size >= cha.length){
			return ;
		}
		reverse(cha,0,size-1);
		reverse(cha,size,cha.length - 1);
		reverse(cha,0,cha.length - 1);
	}
	
	/**
	 * @author Ethan
	 * @desc 多次左右交换
	 */
	public void rotateBySwap(char[] cha,int size){
		if(cha == null || cha.length == 0 || size <= 0 || size >= cha.length){
			return ;
		}
		int start = 0;
		int end = cha.length - 1;
		int lpart = size;
		int rpart = cha.length - size;
		int s = Math.min(lpart, rpart);
		int d = lpart - rpart;
		
		while(true){
			exchange(cha,start,end,size);
			if(d == 0){
				break;
			}else if(d > 0){
				start += s;
				lpart = d;
			}else{
				end -= -d;
				rpart = -d;
			}
			s = Math.min(lpart, rpart);
			d = lpart - rpart;
		}
	}
	
	private void exchange(char[] cha, int start, int end, int size) {
		int i = end - size + 1;
		char tmp = 0;
		while(size-- != 0){
			tmp = cha[i];
			cha[i] = cha[start];
			cha[start] = tmp;
			start++;
			i++;
		}
	}

	private void reverse(char[] cha, int start, int end) {
		char tmp = 0;
		while(start < end){
			tmp = cha[end];
			cha[end] = cha[start];
			cha[start] = tmp;
			start++;
			end--;
		}
	}
}

```
