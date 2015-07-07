##  java lession note 07

* 01  `匿名类` 创建的是对应类的派生类 ，可以覆盖某些方法 ，实现新的逻辑 ；由于没有对应派生类的类名， 新增的方法不方便访问
> 匿名类建议不要定义太长 ；可以使用初始化代码 ； 一次性使用 ;没有构造函数（名字都没有）
> 匿名类应该是具体类 ，如果有抽象方法 ，需要全部实现

* 02  参照`匿名类`的思路，可以写出匿名接口
> 一次只能实现一个接口

* 03  内部类 就是一个类的内部还包含着另一个类；
> 缺点： 破坏良好的代码结构
> 优点： 内部类可随意使用外部类的成员变量（包括私有）而不用生成外部类的对象
> 非静态内部类中 ，不允许声明任何静态成员

* 04  内部类体现了一中类的嵌套关系 ，this为最深一级的类的实例引用， 对外部类的this引用加上类名前缀
```java
class Out{
	int aa;
	class In{
		int aa;
		{
			this.aa = 4;
			Out.this.aa = 5;
		}
	}
}
```

* 05	函数内部也可以定义类 ，需先声明后使用; 可以以只读方式使用函数的局部变量和参数 ，不允许修改值
* 06  Thread 通过实现了Runnable  接口的类 或者字符串 或者线程组 构造
* 07  Thread start() stop() suspend() resume()
> 除了第一个 ，其他都不安全 ，（已经废弃？ 见api)

* 08  指派给线程的任务需要封装在实现了Runnable 接口的类的实例的run()函数中, 然后以此实例，生成Thread..
* 09  具体一点的生成方法
	 *  额外创建类， 实现Runnable 接口， 生成 Thread
	 *  额外创建类， 继承Thread 类， 重写run 方法, 之后直接new 即可
   *  创建匿名类， 实现Runnable 接口， 成成 Thread
   *  创建匿名类， 派生自Thread， 重写run 方法， 之后直接使用
	 *  注： 12,34 仅仅在语句书写上不同，本质一样(吧..)
* 10  一个线程对象只能调用一次start, 可以多次调用run， start一次后就不能用了
* 11  Thread.yield() 本次让出cpu时间片， 由运行-> 就绪，等待下次调度
* 12  虚拟机退出(System.exit()或者 main执行结束):  这时候如果有用户线程（非守护线程），则等它执行完； 如果只有守护线程，可以退出，不论它执行到哪里
* 13  多线程并发访问共享数据， 造成不安全；线程函数内局部变量则不需要保护，不会引起冲突
* 14  对象锁 是互斥锁； 所有对象都自动含有
* 15  解决冲突： 1. 锁机制  2. 对象复制
* 16  synchronized 相当于信号量的wait操作, 参数是一个对象， 实际使用这个对象的对象锁（互斥锁）； 对象锁自动释放，不需要显式sinal操作; 与声明同步函数相比， 仅对临界区代码声明synchronized 更加高效
```java
public void testSync(){
  int a = 0;
	//do sth..剩余区
	synchronized(this){
		//do sth.. 临界区
	}
}
```

* 17  对阻塞条件的判断，建议使用while 而不是if ,（因为解除阻塞后不一定可以获得执行，需要持续监视条件）
* 18  不同的逻辑，往往需要使用多个锁，所以需要生成多个对象(提供锁）；
> 姜老师建议对象: Object lock = new byte[0]; 据说这个很快..
* 19  关于 wait, notify 之类的， 暂时还没懂..

