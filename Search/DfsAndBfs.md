>深度优先和广度优先

- 搜索原理

```
/**
 * @author Ethan
 * @desc
 * @date 2017年8月16日
 */
public class DfsAndBfs {
	/*
	 * vertexs:存储顶点 adjVertexs:存储顶点连接关系
	 * */
	private int MAX;
	private Vertex[] vertexs;
	private int[][] adjVertexs;
	private StackX stack;
	private QueueY queue;
	
	private int tempId;
	
	public DfsAndBfs(int num){
		this.MAX = num;
		vertexs = new Vertex[num];
		adjVertexs = new int[num][num];
		stack = new StackX(num);
		queue = new QueueY(num);
	}
	
	/**
	 * @desc 基于栈的深度优先搜索
	 */
	public void dfsByStack(){
		operateVertex(0,1);
		//基于栈的出栈入栈开始搜索
		while(!stack.isEmpty()){
			tempId = getAdjFirstUnvisitedVertex(stack.peek());
			if(tempId == -1){
				stack.pop();
			}else{
				operateVertex(tempId,1);
			}
		}
		initVertexs();
	}


	/**
	 * @desc 基于队列的广度优先搜索
	 */
	public void bfsByQueue(){
		operateVertex(0,-1);
		while(!queue.isEmpty()){
			tempId = queue.remove();
			int adjId;
			while((adjId = getAdjFirstUnvisitedVertex(tempId)) != -1){
				operateVertex(adjId,-1);
			}
		}
		initVertexs();
	}

	/**
	 * @desc 搜索完后，重新初始化顶点数组 
	 */
	private void initVertexs() {
		for(int i = 0; i < MAX; i++){
			vertexs[i].isVisited = false;
		}
	}
	/**
	 * @desc 返回邻接矩阵中第一个未被访问的顶点
	 * @param id 
	 * @return int:第一个未被访问的顶点id -1:无
	 */
	private int getAdjFirstUnvisitedVertex(int id) {
		for(int i = 0; i < MAX; i++){
			if(adjVertexs[id][i] == 1 && vertexs[i].isVisited == false){
				return i;
			}
		}
		return -1;
	}

	/**
	 * @desc 操作顶点
	 * @param id 被操作的顶点id
	 * @param flag 1:栈 2:队列
	 */
	private void operateVertex(int id, int flag) {
		vertexs[id].isVisited = true;
		showVertex(id);
		if(flag == 1){
			stack.push(id);
		}else{
			queue.insert(id);
		}
	}
	
	/**
	 * @desc 告知顶点被访问
	 * @param id
	 */
	private void showVertex(int id) {
		System.out.println(id + " " + vertexs[id].isVisited);
	}

	/**
	 * @desc 初始化图
	 */
	public void initGraph(){
		//添加顶点
		for(int i = 0; i < MAX; i++){
			addVertex(i);
		}
		addEdge(0,1);
		addEdge(0,2);
		addEdge(0,3);
		addEdge(1,4);
		addEdge(1,5);
		addEdge(2,6);
		addEdge(4,7);
		
		showAdjVertexs();
	}
	
	/**
	 * @desc 打印邻接矩阵
	 */
	private void showAdjVertexs() {
		for(int i=0;i<MAX;i++){
			System.out.println();
			for(int j=0;j<MAX;j++){
				System.out.print(adjVertexs[i][j]+" ");
			}
		}
	}

	/**
	 * @desc 加边
	 * @param start 源点
	 * @param end 终点
	 */
	private void addEdge(int start, int end) {
		adjVertexs[start][end] = 1;
		adjVertexs[end][start] = 1;
	}

	/**
	 * @desc 加点
	 * @param i：点的id
	 */
	private void addVertex(int i) {
		vertexs[i] = new Vertex(i);
	}

	public static void main(String[] args) {
		DfsAndBfs dab = new DfsAndBfs(8);
		System.out.println("初始化图");
		dab.initGraph();
		System.out.println("深度优先搜索");
		dab.dfsByStack();
		System.out.println("广度优先搜索");
		dab.bfsByQueue();
		
	}
}

/**
 * @author Ethan
 * @desc 顶点类：描述图中顶点
 * @date 2017年8月16日
 */
class Vertex{
	public int id;
	public boolean isVisited;
	
	public Vertex(int id){
		this.id = id;
	}
}

/**
 * @author Ethan
 * @desc 基于数组的栈：实现深度优先遍历
 * @date 2017年8月16日
 */
class StackX{
	/*
	 * MAX:数组长度 top:顶点指针
	 * */
	private int MAX;
	private int[] arr;
	private int top = -1;
	
	public StackX(int num){
		this.MAX = num;
		arr = new int[num];
	}
	
	/**
	 * @desc 压栈
	 * @param value 压栈值
	 * @return boolean 是否压栈成功
	 */
	public boolean push(int value){
		arr[++top] = value;
		return true;
	}
	
	/**
	 * @desc 出栈
	 * @return int -1：栈空
	 */
	public int pop(){
		if(!isEmpty()){
			return arr[top--];
		}
		return -1;
	}
	
	/**
	 * @desc 返回栈顶元素
	 * @return -1：栈空
	 */
	public int peek(){
		if(!isEmpty()){
			return arr[top];
		}
		return -1;
	}
	
	/**
	 * @desc 判断栈是否为空
	 * @return boolean ture:空
	 */
	public boolean isEmpty(){
		return top == -1;
	}
}


/**
 * @author Ethan
 * @desc 基于数组的队列：实现广度优先遍历
 * @date 2017年8月16日
 */
class QueueY{
    /*
     * MAX:数组最大长度 front:头指针 rear:尾指针
     * */
	private int MAX;
	private int[] arr;
	private int front;
	private int rear = -1;
	
	public QueueY(int num){
		this.MAX = num;
		arr = new int[num];
	}
	
	/**
	 * @desc 插入值
	 * @param value 值
	 * @return boolean true:插入成功
	 */
	public boolean insert(int value){
		arr[++rear] = value;
		if(rear == MAX - 1){
			rear = -1;
		}
		return true;
	}
	
	/**
	 * @desc 队列移除
	 * @return int:移除值
	 */
	public int remove(){
		int temp = arr[front++];
		if(front == MAX){
			front = 0;
		}
		return temp;
	}
	
	/**
	 * @desc 队列是否为空:两种情况
	 * @return boolean true:队列空
	 */
	public boolean isEmpty(){
		return rear + 1 == front;
	}
}
```
