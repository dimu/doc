# java design pattern #

##创建模式##

以下几个模式通常出现在对象的创建过程中：

###Factory###
工厂模式中主要是创建对象。在有些对象创建过程中有很多初始化条件，这种全部耦合到构造函数中，在每次生成对象时都特别复杂。

    public class Factory{
	public static Sample creator(int which){
	//getClass 产生Sample 一般可使用动态类装载装入类。
	if (which==1)
		return new SampleA();
	else if (which==2)
		return new SampleB();
	}}


###Abstract Factory###

	`public abstract class ForumFactory {
		private static Object initLock = new Object();
		private static String className = "com.jivesoftware.forum.database.DbForumFactory";
		private static ForumFactory factory = null; 
		
		public static ForumFactory getInstance(Authorization authorization) {
		//If no valid authorization passed in, return null.
		if (authorization == null) {
			return null;
		}
		//以下使用了Singleton 单态模式
		if (factory == null) {
			synchronized(initLock) {
				if (factory == null) {
					...... 
					try {
						//动态转载类
						Class c = Class.forName(className);
						factory = (ForumFactory)c.newInstance();
				}	catch (Exception e) {
				return null;
				}
			}
		}}
		//Now, 返回 proxy.用来限制授权对forum的访问
		return new ForumFactoryProxy(authorization, factory,factory.getPermissions(authorization));
	}
	
	//真正创建forum的方法由继承forumfactory的子类去完成.
	public abstract Forum createForum(String name, String description)	throws UnauthorizedException, ForumAlreadyExistsException;
	}

`

###Prototype###

原型：用原型实例指定创建对象的种类，并且通过拷贝这些原型创建新的对象。
    
	package prototype;

	public abstract class AbstractSpoon implements Cloneable {
	String spoonName;

	public void setSpoonName(String spoonName) {
		this.spoonName = spoonName;
	}
	
	public String getSpoonName() {return this.spoonName;}
	
	/**
	 * 实现clone操作
	 */
	public Object clone(){
		Object object = null;
		try {
			object = super.clone();
		} catch (CloneNotSupportedException exception) {
			System.err.println("AbstractSpoon is not Cloneable");
		}
		return object;
	}
	
	public static void main(String[] args) {
		AbstractSpoon soup = new SoupSpoon();
		Object soupClone = soup.clone();
		if (soupClone instanceof SoupSpoon) {
			System.out.println("clone object is SoupSpoon instance"); //运行结果ok
			System.out.println(((SoupSpoon) soupClone).getSpoonName());
		}
	}
	}

	class SoupSpoon extends AbstractSpoon
	{ 
	public SoupSpoon()
	{
		setSpoonName("Soup Spoon");
	}
	}
	class SaladSpoon extends AbstractSpoon{ 
	public SaladSpoon(){
		setSpoonName("Salad Spoon");
	}
	}



###Singleton###

单例是很重要的，在应用程序中只有1个对象

	`package singleton;


	public class Singleton {
	private static Singleton instance = new Singleton();
	
	/**
	 * 构造函数私有避免实例化对象
	 * Singleton.java constructor
	 */
	private Singleton(){
		
	}

	//这里提供了一个供外部访问本class的静态方法，可以直接访问　　
	public static Singleton getInstance() {
		return instance;
	}
	} 


	class Singleton1 {
	
	private static Singleton1 instance;
	
	public static synchronized Singleton1 getInstance( ) {
		if (null ==  instance) {
			instance = new Singleton1();
		}
		
		return instance;
	}
	}

	 
`

###Builder###

builder模式将结果与生成过程分离，例如汽车需要很多零部件，然后最后组装起来，

## 结构模式 ##

###Facade###

facade：外观模式 ，为子系统的接口提供一致的定义。

### Proxy ###

代理模式是一种常见的模式，非常重要，理解为从出发点到最终目标添加了一层中间层。代理可以作为一种网关控制或者对访问资源的控制。

###Adapter###

适配器：将两个不相关的类在一起使用。一般来说都是实现两个接口，将两个接口的实现类注入进来，然后再adapter中使用，使用到了组合与继承。

###composite###

组合模式：将对象以树形结构组织起来，以达成“部分-整体”的层次结构，使得客户端对单个对象和组合对象的使用具有一致性。

###decorator###
装饰模式：动态的给对象增加功能，如果是采用子类继承有时候很繁琐，就采用decorator.
装饰模式有点像病毒入侵的形式。

### Bridge ###

###Flyweight###


##行为模式##

##template##

将实现放在子类去完全，父类搭好框架。

###Memento###
备忘机制：是一个保存另外一个对象内部状态拷贝的对象，这样可以将对象恢复到原先保存的样子，不过内存开销很大，一般不推荐使用。

## ##