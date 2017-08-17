>单例类只有一个实例，且只能自己创建这个实例，并且为所有对象提供这个实例；

1. 懒汉式(第一次调用时实例化)

- 懒汉式(线程不安全)

```
/**
 * @author Ethan
 * @desc 懒汉式单例
 * @date 2017年8月17日
 */
public class Singleton {
	private static Singleton singleton = null;
	
	private Singleton(){}
	
	public static Singleton getInstance(){
		if(singleton == null){
			singleton = new Singleton();
		}
		return singleton;
	}
}
```

- 实例方法上添加同步锁(多次同步限制性能)

```
	public static synchronized Singleton getInstance(){
		if(singleton == null){
			singleton = new Singleton();
		}
		return singleton;
	}

```

- 双重校验(仅第一次调用时产生同步)

```
	public static Singleton getInstance(){
		if(singleton == null){
			synchronized(Singleton.class){
				if(singleton == null){
					singleton = new Singleton();
				}
			} 
		}
		return singleton;
	}
```

- 静态内部类(利用classloader加载时的单线程安全性)

```
public class Singleton{

	private static class LazyHolder{
		private static final Singleton INSTANCE= new Singleton();
	}

	private Singleton(){}
	
	public static final Singleton getInstance(){
		return LazyHolder.INSTANCE;
	}
}

```

2. 饿汉式(初始化是实例化)

```
/**
 * @author Ethan
 * @desc 饿汉式单例
 * @date 2017年8月17日
 */
public class Singleton{
	private static Singleton singleton = new Singleton();
	
	private Singleton(){}
	
	public static Singleton getInstance(){
		return singleton;
	}
}
```
