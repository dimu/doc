# Default Method Res #

default method 也叫defender方法或者虚拟扩展方法（virtual extension methods）

## 示例代码 ##

**接口定义**
    
	public interface DefaultMethodInterface {
	
	/**
	 * description: 定义的正常消息接口
	 * @param msg 输出的消息
	 * @time: 2017年5月4日 下午3:21:50
	 */
	void sayMessage(String msg);
	
	/**
	 * description: 默认函数（defender函数）
	 * @param msg 输出的异常消息
	 * @time: 2017年5月4日 下午3:21:12
	 */
	default void sayError(String msg) {
		System.out.println("error msg :" + msg);
	}}

**接口实现**
    
	public class Java8DefaultMethod implements DefaultMethodInterface{

	@Override
	public void sayMessage(String msg) {
		System.out.println("normal message : " + msg);
	}

	@Test
	public void defaultMethodTest() {
		sayMessage("hello word");
		sayError("null pointer exception");
	}}

## 应用场景 ##

1. 扩展原有接口——针对原有接口进行功能扩展，不需要修改实现类。
2. 提供默认实现，无须每个接口的实现类都实现相同的功能。
3. 在spring framework5.0版本webmvc的适配器WebMvcConfigureAdapter就被废弃掉，其功能被WebMvcConfigurer接口采用default method接口实现了，所以springframework中许多Adapter抽象类就被默认接口实现给替换了。