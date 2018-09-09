```
package Chapter8;

/**
 * @author Ethan
 * @desc 返回数组中子数组累乘最大的结果 
 */
public class C8MaxMultiInArr {

	/**
	 * @author Ethan
	 * @desc 计算以每一个数组元素结尾的最大值 
	 */
	public double maxMulti(double[] num){
		//1-异常参数检测
		if(num == null || num.length == 0){
			return 0;
		}
		//2-初始化 max: min: res:
		double max = num[0];
		double min = num[0];
		double res = num[0];
		//3-遍历数组
		for(int i = 1; i < num.length; i++){
			max = max * num[i];
			min = min * num[i];
			max = Math.max(Math.max(max, min),num[i]);
			min = Math.min(Math.min(max, min),num[i]);
			res = Math.max(max, res);
		}
		return res;
	}
	
	public static void main(String[] args) {
		C8MaxMultiInArr mmia = new C8MaxMultiInArr();
		double[] num = {-2.5,4,0,3,0.5,8,-1};
		double res = mmia.maxMulti(num);
		System.out.println(res);
	}
}

```
