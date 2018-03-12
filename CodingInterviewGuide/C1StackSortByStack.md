>题目

借助一个辅助栈和一个变量，不能申请其他数据结构，实现栈从顶到下降序排序；

- 实现

（1）curr:记录每次弹出栈元素，stack:原始栈 help:辅助栈

（2）curr大于等于help栈顶元素直接压栈，否则将help中元素逐一压入stack中，直到curr大于等于help栈顶元素；

```
import java.util.Stack;

/**
 * @author Ethan
 * @desc 借助栈和一个变量实现栈的从顶到下降序排序
 */
public class C1StackSortByStack {
	
	public Stack<Integer> stack;
	
	public C1StackSortByStack(){
		stack = new Stack<Integer>();
	}
	
	/**
	 * @author Ethan
	 * @desc 借助临时变量存储弹出值
	 */
	public void stackSortByStack(){
		//初始化辅助栈
		Stack<Integer> help = new Stack<Integer>();
		//循环至stack为空
		while(!stack.isEmpty()){
			//curr:记录当前弹出的元素
			int curr = stack.pop();
			while(!help.isEmpty() && help.peek() < curr){
				stack.push(help.pop());
			}
			help.push(curr);
		}
		//将help中元素出栈逐一压入stack中
		while(!help.isEmpty()){
			stack.push(help.pop());
		}
	}
}

```
