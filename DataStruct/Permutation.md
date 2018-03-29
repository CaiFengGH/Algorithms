>题目描述

实现字符串的全排列

- 方法实现

选取一个字符作为前缀，实现交换后，对剩余字符串进行全排列，这是一个递归实现的过程；

```
package DayCode;

/**
 * @author Ethan
 * @desc 实现字符串的全排列 
 */
public class Permutation {

	public void permutation(char[] cha,int from,int to){
		//1-异常参数判断和递归结束条件
		if(to <= 1){
			return ;
		}else if(from == to){
			System.out.println(String.valueOf(cha));
		}else{
			for(int i = from; i <= to; i++){
				//获取前缀，交换位置
				swap(cha,i,from);
				//递归执行
				permutation(cha,from+1,to);
				//将位置再次返回回来
				swap(cha,from,i);
			}
		}
	}

	private void swap(char[] cha, int from, int i) {
		char tmp = cha[from];
		cha[from] = cha[i];
		cha[i] = tmp;
	}
}

```
