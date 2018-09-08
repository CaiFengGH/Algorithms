```
package Chapter8;

import java.util.LinkedList;
import java.util.Queue;

public class MinPathSum {

	/**
	 * @author Ethan
	 * @desc 返回二维数组中的最短路径值
	 */
	public int minPathSum(int[][] m){
		//1-异常参数检测
		if(m == null || m.length == 0 || m[0].length == 0
				|| m[0][0] != 1 || m[m.length - 1][m[0].length - 1] != 1){
			return 0;
		}
		//2-初始化 map:到达ij的最短路径
		int[][] map = new int[m.length][m[0].length];
		map[0][0] = 1;
		
		//rowQueue:行队列 colQueue:列队列 
		Queue<Integer> rowQueue = new LinkedList<Integer>();
		Queue<Integer> colQueue = new LinkedList<Integer>();
		rowQueue.add(0);
		colQueue.add(0);
		
		int row = 0;
		int col = 0;
		
		//3-循环弹出队列
		while(!rowQueue.isEmpty()){
			row = rowQueue.poll();
			col = colQueue.poll();
			
			if(row == m.length - 1 && col == m[0].length - 1){
				return map[row][col];
			}
			//向上
			walkTo(map[row][col],row-1,col,map,m,rowQueue,colQueue);
			//向下
			walkTo(map[row][col],row+1,col,map,m,rowQueue,colQueue);
			//向左
			walkTo(map[row][col],row,col-1,map,m,rowQueue,colQueue);
			//向右
			walkTo(map[row][col],row,col+1,map,m,rowQueue,colQueue);
		}
		return 0;
	}

	/**
	 * @author Ethan
	 * @desc 移动到下一步 
	 */
	private void walkTo(int pre, int toRow, int toCol, int[][] map, int[][] m,
			Queue<Integer> rowQueue, Queue<Integer> colQueue) {
		//1-异常参数检测 
		if(toRow < 0 || toRow == m.length || toCol < 0 || toCol == m[0].length
				|| m[toRow][toCol] != 1 || map[toRow][toCol] != 0){
			return ;
		}
		//2-移动下一步
		map[toRow][toCol] = pre + 1;
		rowQueue.add(toRow);
		colQueue.add(toCol);
	}
	
	public static void main(String[] args) {
		MinPathSum mps = new MinPathSum();
		int[][] m = {{1,1,1,1,1},{1,0,1,0,1},{1,1,1,0,1},{0,0,0,0,1}};
		int res = mps.minPathSum(m);
		System.out.println(res);
	}
}
```
