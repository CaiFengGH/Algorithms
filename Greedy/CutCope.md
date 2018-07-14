- 减绳子问题

给你一个长度为n的绳子，请把绳子剪成m段（m，n都是整数，且都大于1）每段绳子的长度即为K[0],K[1],K[2]...K[m]请问K[0]*k[1]..*k[m]可能的最大乘积是多少 ? 

关键：n >= 5，剪去3的倍数，余下为4，则拆分为2*2；

链接：[贪心算法之基础](https://www.cnblogs.com/MrSaver/p/8641971.html)
[贪心算法之场景](https://blog.csdn.net/a345017062/article/details/52443781)

```
package DayCode;

/**
 * @author Ethan
 * @desc 
 * 给你一个长度为n的绳子，请把绳子剪成m段（m，n都是整数，且都大于1）
 * 每段绳子的长度即为K[0],K[1],K[2]...K[m]
 * 请问K[0]*k[1]..*k[m]可能的最大乘积是多少 ? 
 */
public class CutCope {

	/**
	 * @author Ethan
	 * @desc 基于贪心算法实现
	 */
	public double cutCopeMaxMulti(int n){
		//1-异常参数检测
		if(n < 2){
			return 0;
		}
		if(n == 2){
			return 2;
		}
		if(n == 3){
			return 3;
		}
		if(n == 4){
			return 4;
		}
		//2-整除以3
		int numOf3 = n / 3;
		//3-判断余数大小 余数为1 则拆分成2*2
		if(n - numOf3 * 3 == 1){
			numOf3 -= 1;
		}
		int numOf2 = (n - numOf3 * 3) / 2;
		//4-获得最后的乘积
		double res = Math.pow(3, numOf3) * Math.pow(2, numOf2);
		return res;
	}

	public static void main(String[] args) {
		
		CutCope cc = new CutCope();
		System.out.println(cc.cutCopeMaxMulti(7));
	}
}

```
