```
package Chapter8;

/**
 * @author Ethan
 * @desc 顺时针由外向内打印矩阵
 */
public class C8ClockwisePrint {

	/**
	 * @author Ethan
	 * @desc 以矩阵左上角元素坐标和右下角元素坐标打印 
	 */
	public void clockwisePrint(int[][] matrix){
		//1-初始化坐标
		int upperLeftRow = 0;
		int upperLeftCol = 0;
		int lowerRightRow = matrix.length - 1;
		int lowerRightCol = matrix[0].length - 1;
		
		//2-由外向内打印
		while(upperLeftRow <= lowerRightRow 
				&& upperLeftCol <= lowerRightCol){
			printCircle(matrix,upperLeftRow++,upperLeftCol++,
					lowerRightRow--,lowerRightCol--);
		}
	}
	
	/**
	 * @author Ethan
	 * @desc 顺时针打印一圈
	 */
	public void printCircle(int[][] matrix,int upperLeftRow,int upperLeftCol,
			int lowerRightRow,int lowerRightCol){
		//1-仅为一行时
		if(upperLeftRow == lowerRightRow){
			for(int i = upperLeftCol; i <= lowerRightCol; i++){
				System.out.print(matrix[upperLeftRow][i] + " ");
			}
		}
		//2-仅为一列时
		else if(upperLeftCol == lowerRightCol){
			for(int i = upperLeftRow; i <= lowerRightRow; i++){
				System.out.print(matrix[i][upperLeftCol] + " ");
			}
		}
		//3-多行多列(包括一行多列或者多行一列)
		else{
			int curRow = upperLeftRow;
			int curCol = upperLeftCol;
			//从左向右移动
			while(curCol != lowerRightCol){
				System.out.print(matrix[curRow][curCol++] + " ");
			}
			//从上向下移动
			while(curRow != lowerRightRow){
				System.out.print(matrix[curRow++][curCol] + " ");
			}
			//从右向左移动
			while(curCol != upperLeftCol){
				System.out.print(matrix[curRow][curCol--] + " ");
			}
			//从下向上移动
			while(curRow != upperLeftRow){
				System.out.print(matrix[curRow--][curCol] + " ");
			}
		}
	}
}

```
