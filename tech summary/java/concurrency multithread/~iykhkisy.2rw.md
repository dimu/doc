# Java Concurrency and multi thread #

## 常见的实现线程方式 ##

**定义任务（实现runnable接口），然后由Thread来驱动**

    
	    public class LiftOff implements Runnable {
    	protected int countDown = 10; // Default
    	private static int taskCount = 0;
    	private final int id = taskCount++;
    
    	public LiftOff() {
    	}
    
    	public LiftOff(int countDown) {
    		this.countDown = countDown;
    	}
    
    	public String status() {
    		return "#" + id + "(" + (countDown > 0 ? countDown : "Liftoff!") + "), ";
    	}
    
    	public void run() {
    		while (countDown-- > 0) {
    			System.out.print(status());
    			Thread.yield();
    		}
    	}
    	
    	public static void main(String[] args) {
    		new Thread(new LiftOff(10)).start();
    	}
    	} 

runnable任务并不具备任何线程能力，如果要具备线程能力必须将任务添加到线程上。

**集成Thread类**
由于java是单一继承，如果继承了Thread类后就不能继承其他类了，所以一般优先实现Runnable接口


**使用Executor（执行器）**

java1.5新增了并发类，优先推荐使用Excutor来管理Thread对象。

常见的ExecutorService：CachedThreadPool, FixedThreadPool,SingleThreadExecutor，ScheduledThreadPool等。

代码示例：

    public class FixedThreadExecutor {
	public static void main(String[] args) {
		ExecutorService exec = Executors.newFixedThreadPool(5);
		for(int i = 0; i < 5; i++){
			exec.execute(new LiftOff());
		}
		exec.shutdown();
	}

	}

**从任务中产生返回值**

传统的实现runnable接口并不能从任务中产生返回值，但是有些业务需求需要监控任务执行情况，就需要返回运行结果。
jdk1.5引入java.util.concurrency.Callable<T>接口来产生返回值。

例子：

    class TaskWithResult implements Callable<String> {
	private int id;

	public TaskWithResult(int id) {
		this.id = id;
	}

	public String call() {
		return "result of TaskWithResult " + id;
	}
	}

	public class CallableDemo {
	public static void main(String[] args) {
		ExecutorService exec = Executors.newCachedThreadPool();
		List<Future<String>> results = new ArrayList<Future<String>>();
		for (int i = 0; i < 10; i++)
			results.add(exec.submit(new TaskWithResult(i)));
		for (Future<String> fs : results)
			try {
				// get() blocks until completion:
				System.out.println(fs.get());
			} catch (InterruptedException e) {
				System.out.println(e);
				return;
			} catch (ExecutionException e) {
				System.out.println(e);
			} finally {
				exec.shutdown();
			}
	}
	}

**休眠方式**

jdk1.5以前方式：

Thread.sleep(1000)

jdk1.5开始及以后方式：

TimeUnit.MILLISECONDS.sleep(1000)

**后台线程**

deamon线程是指程序运行的时候在后台提供一种通用服务的线程，并且这种线程不属于程序中不可或缺的部分，
当程序所有非后台线程结束时，程序也就终止了，同时杀死进程中所有的后台线程。

**加入一个线程**

在当前线程中调用另外一个线程的thread.join()方法，当前线程将被挂起，等待加入的线程运行结束或者超时后再
被唤醒继续运行。

## 资源竞争 ##

**解决共享资源竞争**

常见的方式：
1、使用synchronized关键字进行同步

    public synchronized int next() {}

2、使用显示的lock对象

	......
	
	private Lock lock = new ReentrantLock();

	public int next() {

		lock.lock();

		try {
		  .....
		  return number;
		} finally {
			lock.unlock();
		}

**原子类**	

JAVA SE5引入了AtomicInteger，AtomicLong, AtomicReference等特殊的原子类，即使使用了原子类也存在并发风险，
在要求很高的情况下还是使用synchronized或者lock锁 

**临界区**

使用同步控制块，而不是使用synchronized关键字锁住整个方法，这样尽可能的减少同步区域，提高并发效率

**线程本地存储**

