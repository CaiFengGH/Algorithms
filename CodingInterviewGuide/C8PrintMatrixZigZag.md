```
package Chapter8;

/**
 * @author Ethan
 * @desc 之字形打印矩阵
 */
public class C8PrintMatrixZigZag {

	/**
	 * @author Ethan
	 * @desc 移动对角线指标
	 */
	public void move(int[][] matrix){
		//1-初始化
		int upperLeftRow = 0;
		int upperLeftCol = 0;
		int lowerRightRow = 0;
		int lowerRightCol = 0;
		
		int rows = matrix.length - 1;
		int cols = matrix[0].length - 1;
		
		//方向从上往下:false 从下往上:true
		boolean direction = true;
		
		//2-移动打印，截止条件是upperLeftRow != rows + 1
		while(upperLeftRow != rows + 1){
//			System.out.println(upperLeftRow + " " + upperLeftCol + " "+ lowerRightRow + " " + lowerRightCol + " ");
			printZigZag(matrix,upperLeftRow,upperLeftCol,
					lowerRightRow,lowerRightCol,direction);
			//更新四个指标
			upperLeftRow = upperLeftCol == cols ? upperLeftRow + 1 : upperLeftRow;
			upperLeftCol = upperLeftCol == cols ? cols : upperLeftCol + 1;
			
			//下面两条语句顺序不能置换，因为比较变量中值发生变化
			lowerRightCol = lowerRightRow == rows ? lowerRightCol + 1 : lowerRightCol;
			lowerRightRow = lowerRightRow == rows ? rows : lowerRightRow + 1; 
			
			direction = !direction;
		}
		System.out.println();
	}
	
	/**
	 * @author Ethan
	 * @desc 之字形打印
	 */
	public void printZigZag(int[][] matrix,int upperLeftRow,int upperLeftCol,
			int lowerRightRow,int lowerRightCol,boolean direction){
		if(direction){
			while( lowerRightRow != upperLeftRow - 1){
				System.out.print(matrix[lowerRightRow--][lowerRightCol++] + " ");
			}
		}else{
			while( upperLeftRow != lowerRightRow + 1){
				System.out.print(matrix[upperLeftRow++][upperLeftCol--] + " ");
			}
		}
//		System.out.println();
	}
}
```
