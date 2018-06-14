```
package Chapter9;

/**
 * @author Ethan
 * @desc 判断点是否在三角形内部
 * 从任意顶点出发，逆时针旋转，叉积为正，则在三角形内部，
 * 如图所示：
 *     a
 *    /\
 *   / .\
 *  /_o__\
 * b      c
 * 向量ab和向量ao叉积为正，则从a逆时针旋转时为，在内部 
 */
public class C9IsInTriangle {
	
	public boolean isdoubleriangle(double a1,double a2,double b1,double b2,
			double c1,double c2,double o1,double o2){
		
		//1-输入参数逆时针顺序调整
		if(crossProduct(c1-a1,c2-a2,b1-a1,b2-a2) >= 0){
			double tmp1 = b1;
			double tmp2 = b2;
			b1 = c1;
			b2 = c2;
			c1 = tmp1;
			c2 = tmp2;
		}
		
		//2-ab向量
		if(crossProduct(b1-a1,b2-a2,o1-a1,o2-a2) < 0){
			return false;
		}
		
		//3-bc向量
		
		if(crossProduct(c1-b1,c2-b2,o1-b1,o2-b2) < 0){
			return false;
		}
		//4-ca向量
		if(crossProduct(c1-a1,c2-a2,o1-a1,o2-a2) < 0){
			return false;
		}
		
		return true;
	}
	
	/**
	 * @author Ethan
	 * @desc 叉积遵守右手螺旋定则
	 */
	public double crossProduct(double x1,double y1,double x2,double y2){
		return x1 * y2 - x2 * y1;
	}
}
```
