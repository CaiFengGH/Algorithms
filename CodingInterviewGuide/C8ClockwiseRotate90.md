```
package Chapter8;

/**
 * @author Ethan
 * @desc 将N*N的正方形矩阵旋转90度 
 */
public class C8ClockwiseRotate90 {

	/**
	 * @author Ethan
	 * @desc 从外向内分圈移动
	 */
	public void clockwiseRotate90(int[][] matrix){
		//1-初始化坐标
		int upperLeftRow = 0;
		int upperLeftCol = 0;
		int lowerRightRow = matrix.length - 1;
		int lowerRightCol = matrix[0].length - 1;
		
		//2-由外向内打印
		while(upperLeftRow < lowerRightRow){ 
			moveAssign(matrix,upperLeftRow++,upperLeftCol++,
					lowerRightRow--,lowerRightCol--);
		}
	}
	
	/**
	 * @author Ethan
	 * @desc 
	 */
	public void moveAssign(int[][] matrix,int upperLeftRow,int upperLeftCol,
			int lowerRightRow,int lowerRightCol){
		//1-初始化times
		int times = lowerRightRow - upperLeftRow;
		//2-移动赋值
		for(int i = 0; i < times; i++){
			int tmp = matrix[upperLeftRow][upperLeftCol + i];
			matrix[upperLeftRow][upperLeftCol + i] = matrix[lowerRightRow - i][upperLeftCol];
			matrix[lowerRightRow - i][upperLeftCol] = matrix[lowerRightRow][lowerRightCol - i];
			matrix[lowerRightRow][lowerRightCol - i] = matrix[upperLeftRow + i][lowerRightCol]; 
			matrix[upperLeftRow + i][lowerRightCol] = tmp;
		}
	}
}
```
