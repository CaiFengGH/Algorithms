```
package Chapter8;

import java.util.HashMap;
import java.util.LinkedList;
import java.util.List;
import java.util.Map.Entry;

/**
 * @author Ethan
 * @desc 在数组中找到出现次数大于N/K个 
 */
public class C8FindKMajor {
	
	/**
	 * @author Ethan
	 * @desc n/k类型问题 
	 */
	public void findKMajor(int[] num,int k){
		//1-异常参数检测
		if(num == null || num.length == 0 || num.length < k){
			return;
		}
		
		//2-初始化候选成员
		HashMap<Integer,Integer> cands = new HashMap<Integer,Integer>();
		for(int i = 0; i < num.length; i++){
			//包含key，更新
			if(cands.containsKey(num[i])){
				cands.put(num[i], cands.get(num[i])+1);
			}else{
				//不包含key，为k-1，则所有候选成员减1
				if(cands.size() == k - 1){
					allMinusOne(cands);
				}else{
					//不包含key，不为k-1，则添加候选成员
					cands.put(num[i], 1);
				}
			}
		}
		
		//3-计算每个候选成员出现次数
		HashMap<Integer,Integer> times = getTimes(num,cands);
		
		//4-打印出候选成员次数超过n/k的成员
		boolean hasNum = false;
		int key = 0;
		for(Entry<Integer,Integer> entry : cands.entrySet()){
			key = entry.getKey();
			if(times.get(key) > num.length / k){
				hasNum = true;
				System.out.println(key);
			}
		}
		//5-打印出异常信息
		System.out.println(hasNum ? "" : "没有数字出现n/k次");
	}

	/**
	 * @author Ethan
	 * @desc 统计cands中出现的次数
	 */
	private HashMap<Integer, Integer> getTimes(int[] num,
			HashMap<Integer, Integer> cands) {
		//1-初始化times
		HashMap<Integer,Integer> times = new HashMap<Integer,Integer>(); 
		//2-遍历num
		for(int i = 0; i < num.length; i++){
			int curNum = num[i];
			if(cands.containsKey(curNum)){
				if(times.containsKey(curNum)){
					times.put(curNum, times.get(curNum) + 1);
				}else{
					times.put(curNum, 1);
				}
			}
		}
		return times;
	}

	/**
	 * @author Ethan
	 * @desc 注意集合遍历时，不可作更改集合元素的操作 
	 */
	private void allMinusOne(HashMap<Integer, Integer> cands) {
		List<Integer> remove = new LinkedList<Integer>(); 
		//1-遍历减一
		for(Entry<Integer,Integer> entry : cands.entrySet()){
			int key = entry.getKey();
//			System.out.println(key);
			int value = entry.getValue();
//			System.out.println(value);
			//2-记录value为1的键
			if(value == 1){
				remove.add(key);
			}
			cands.put(key, value-1);
		}
		//3-移除记录的键
		for(Integer i : remove){
			cands.remove(i);
		}
	}
	
	public static void main(String[] args) {
		C8FindKMajor fkm = new C8FindKMajor();
		int[] num = {1,2,3,2,2,1,1,3};
		
		fkm.findKMajor(num, 2);
	}
}
```
