String、StringBuffer、StringBuilder区别
StringBuffer、StringBuilder和String一样，也用来代表字符串。String类是不可变类，任何对String的改变都 会引发新的String对象的生成；StringBuffer则是可变类，任何对它所指代的字符串的改变都不会产生新的对象。既然可变和不可变都有了，为何还有一个StringBuilder呢？相信初期的你，在进行append时，一般都会选择StringBuffer吧！

先说一下集合的故事，HashTable是线程安全的，很多方法都是synchronized方法，而HashMap不是线程安全的，但其在单线程程序中的性能比HashTable要高。StringBuffer和StringBuilder类的区别也是如此，他们的原理和操作基本相同，区别在于StringBufferd支持并发操作，线性安全的，适 合多线程中使用。StringBuilder不支持并发操作，线性不安全的，不适合多线程中使用。新引入的StringBuilder类不是线程安全的，但其在单线程中的性能比StringBuffer高。



接下来，我直接贴上测试过程和结果的代码，一目了然：

```java
public class StringTest {
 
	public static String BASEINFO = "Mr.Y";
	public static final int COUNT = 2000000;
 
	/**
	 * 执行一项String赋值测试
	 */
	public static void doStringTest() {
 
		String str = new String(BASEINFO);
		long starttime = System.currentTimeMillis();
		for (int i = 0; i < COUNT / 100; i++) {
			str = str + "miss";
		}
		long endtime = System.currentTimeMillis();
		System.out.println((endtime - starttime)
				+ " millis has costed when used String.");
	}
 
	/**
	 * 执行一项StringBuffer赋值测试
	 */
	public static void doStringBufferTest() {
 
		StringBuffer sb = new StringBuffer(BASEINFO);
		long starttime = System.currentTimeMillis();
		for (int i = 0; i < COUNT; i++) {
			sb = sb.append("miss");
		}
		long endtime = System.currentTimeMillis();
		System.out.println((endtime - starttime)
				+ " millis has costed when used StringBuffer.");
	}
 
	/**
	 * 执行一项StringBuilder赋值测试
	 */
	public static void doStringBuilderTest() {
 
		StringBuilder sb = new StringBuilder(BASEINFO);
		long starttime = System.currentTimeMillis();
		for (int i = 0; i < COUNT; i++) {
			sb = sb.append("miss");
		}
		long endtime = System.currentTimeMillis();
		System.out.println((endtime - starttime)
				+ " millis has costed when used StringBuilder.");
	}
 
	/**
	 * 测试StringBuffer遍历赋值结果
	 * 
	 * @param mlist
	 */
	public static void doStringBufferListTest(List<String> mlist) {
		StringBuffer sb = new StringBuffer();
		long starttime = System.currentTimeMillis();
		for (String string : mlist) {
			sb.append(string);
		}
		long endtime = System.currentTimeMillis();
		System.out.println(sb.toString() + "buffer cost:"
				+ (endtime - starttime) + " millis");
	}
 
	/**
	 * 测试StringBuilder迭代赋值结果
	 * 
	 * @param mlist
	 */
	public static void doStringBuilderListTest(List<String> mlist) {
		StringBuilder sb = new StringBuilder();
		long starttime = System.currentTimeMillis();
		for (Iterator<String> iterator = mlist.iterator(); iterator.hasNext();) {
			sb.append(iterator.next());
		}
 
		long endtime = System.currentTimeMillis();
		System.out.println(sb.toString() + "builder cost:"
				+ (endtime - starttime) + " millis");
	}
 
	public static void main(String[] args) {
		doStringTest();
		doStringBufferTest();
		doStringBuilderTest();
 
		List<String> list = new ArrayList<String>();
		list.add(" I ");
		list.add(" like ");
		list.add(" BeiJing ");
		list.add(" tian ");
		list.add(" an ");
		list.add(" men ");
		list.add(" . ");
 
		doStringBufferListTest(list);
		doStringBuilderListTest(list);
	}
 
}
```

从上面的结果可以看出，不考虑多线程，采用String对象时（我把Count/100），执行时间比其他两个都要高，而采用StringBuffer对象和采用StringBuilder对象的差别也比较明显。由此可见，如果我们的程序是在单线程下运行，或者是不必考虑到线程同步问题，我们应该优先使用StringBuilder类；如果要保证线程安全，自然是StringBuffer。

从后面List的测试结果可以看出，除了对多线程的支持不一样外，这两个类的使用方式和结果几乎没有任何差别，
