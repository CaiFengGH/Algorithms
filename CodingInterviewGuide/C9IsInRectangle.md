```
package Chapter9;

/**
 * @author Ethan
 * @desc 判断一个点是否在矩形中 
 */
public class C9IsInRectangle {

	/**
	 * @author Ethan
	 * @desc 判断一个点是否在矩形中，特殊情况是平行于x轴和y轴
	 * 将矩阵旋转为 平行于x轴和y轴，然后再进行判断
	 * 最左:x1y1 最上:x2y2 最下:x3y3 最右:x4y4 点:xy
	 *    ______
	 *   |      |
	 *   |   .  |
	 *   |______|
	 * 
	 */
	public boolean isInRectangle(double x1,double y1,double x2,double y2,
			double x3,double y3,double x4,double y4,double x,double y){
		//1-异常参数检测
		if(y1 == y4){
			return isInside(x1, y1, x4, y4, x, y);
		}
		//2-计算右旋角度
		double l = Math.abs(y4 - y3);
		double k = Math.abs(x4 - x3);
		double s = Math.sqrt(l * l + k * k);
		double sin = l / s;
		double cos = k / s;
		//3-更新最左和最右坐标
		double x1R = cos * x1 + sin * y1;
		double y1R = - sin * x1 + cos * y1;
		double x4R = cos * x1 + sin * y1;
		double y4R = - sin * x1 + cos * y1;
		
		//4-更新旋转后坐标
		double xR = cos * x1 + sin * y1;
		double yR = - sin * x1 + cos * y1;
		
		//5-判断
		return isInside(x1R, y1R, x4R, y4R, xR, yR);
	}
	
	/**
	 * @author Ethan
	 * @desc 判断一个点是否位于平行于横纵坐标的矩形内部
	 */
	public boolean isInside(double x1,double y1,double x4,double y4,double x,double y){
		if(x <= x1){
			return false;
		}
		if(x >= x4){
			return false;
		}
		if(y <= y1){
			return false;
		}
		if(y >= y4){
			return false;
		}
		return false;
	}
}

```
