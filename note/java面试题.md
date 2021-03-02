## Java基础-必知必会

### （1） 面向对象可以解释下吗？都有哪些特性？
* 封装：封装隐藏了类的内部实现机制，可以在不影响使用的情况下改变类的内部结构，同时也了保护了数据。对外界而已它的内部细节是隐藏的，暴露给外界的只是它的访问方法。
* 继承：继承是为了重用父类代码。两个类若存在is-a的关系就可以使用继承，同时继承也为实现多态做了铺垫。
* 多态：基于Java的后期绑定机制，程序中引用类型所指的对象的实际类型以及对该对象的方法调用在编译期是不确定的，而是在程序运行中才能确定。然后我们就可以通过继承、实现、重载、重写等机制在不改变原有代码的情况下对程序功能做出修改。

### （2）JDK，JRE和JVM的区别与联系有哪些？
* JVM是Java虚拟机，是Java实现跨平台的关键，帮我们屏蔽了平台差异，当我们运行一个程序时，JVM负责将字节码转换为特定机器代码，同时JVM提供了内存管理、垃圾回收、性能监控、编译优化等功能。
* JRE是Java运行时环境，主要包括JVM和Java类库。
* JDK是Java开发工具包，其中包含JRE，还有一些开发工具如编译器、调试器等。

### （3）抽象类和接口有什么区别？
* 如果类中有抽象方法，那它必须是抽象类，但是抽象类中可以没有抽象方法。
* 接口中除了默认方法之外都是抽象方法。
* 抽象类属于类的范畴，只允许单继承，而接口允许多继承。
* 抽象类中可以存在普通成员变量，接口中只允许出现常量。

### （4）Java中的8种基本数据类型及其取值范围
类型 | 字节 | 位
---- | ---- | ----
byte | 1byte | 8bit
short | 2byte | 16bit
int | 4byte | 32bit
long | 8byte | 64bit
float | 4byte | 32bit
double | 8byte | 64bit
char | 2byte | 16bit
bool | - | -

### （5）Java中的元注解有哪些？
* @Target：指定修饰的注解作用范围（类还、方法、字段、参数等等）。
* @Retention：指定注解保留到什么时候（源码、编译期、运行期）。
* @Documented：指定注解是否可以被标注为公共API。
* @Inherited：指定注解是可被子类继承的。

### （6）说说Java中反射机制
在运行时，通过反射可以获取一个类的各种信息，比如方法、字段、构造函数等，并且对于该类的任意对象，可通过上述信息对其进行修改。所以动态获取信息和动态调用对象方法的功能称为反射机制。

### （7）Java中的Exception和Error有什么区别？
* Error是正常情况下不可能发生的错误，Error会导致JVM处于一种不可恢复的状态，不需要捕获处理，比如说OutOfMemoryError。
* Exception是程序正常运行中预料到可能会出现的错误，并且应该被捕获并进行相应的处理，是一种异常现象，其中有分为编译时异常和运行时异常。
  * 编译时异常（受检异常）表示当前调用的方法体内部抛出了一个异常，所以编译器检测到这段代码在运行时可能会出异常，所以要求我们必须对异常进行相应的处理，可以捕获异常或者抛给上层调用方。
  * 运行时异常（非受检异常）表示在运行时出现的异常，常见的运行时异常包括：空指针异常，数组越界异常，数字转换异常以及算术异常等。

异常捕获规则：
* 尽可能捕获比较详细的异常，而不是使用Exception一起捕获。
* 当本模块不知道捕获之后该怎么处理异常时，可以将其抛给上层模块。
* 捕获异常后至少应该有日志记录，方便之后的排查。
* 不要使用一个很大的try–catch包住整段代码，不利于问题的排查。

NoClassDefFoundError 和 ClassNotFoundException 有什么区别？
* ClassNotFoundException：大概意思就是在说，当我们使用例如Class.forName方法来动态的加载该类的时候，传入了一个类名，但是其并没有在类路径中被找到的时候，就会报ClassNotFoundException异常。出现这种情况，一般都是类名字传入有误导致的。
* NoClassDefFoundError：大概意思是这样的，如果JVM或者ClassLoader实例尝试加载（可以通过正常的方法调用，也可能是使用new来创建新的对象）类的时候却找不到类的定义。但是要查找的类在编译的时候是存在的，运行的时候却找不到了。这个时候就会导致NoClassDefFoundError。出现这种情况，一般是由于打包的时候漏掉了部分类或者Jar包被篡改已经损坏。

### （8）JIT编译器有了解吗？
即时编译器，把经常运行的代码作为"热点代码"编译成与本地平台相关的机器码，并进行各种层次的优化。比如方法内联、逃逸分析、公共子表达式消除、数组边界检查消除等。

包括逃逸分析、锁消除、 锁膨胀、方法内联、空值检查消除、类型检测消除以及公共子表达式消除等。

### （9）String、StringBuffer和StringBuilder的区别？
* 三者都是final的，都不能被继承。
* String长度不可变，其他的长度可变。
* StringBuilder不是线程安全的，StringBuffer时线程安全的。

### （10）Java中的泛型的理解
泛型的本质是参数化类型，即可以将操作的数据类型指定为方法签名中的一种特殊参数，这种类型能够用在类、接口和方法中，分别构成泛型类，泛型接口和泛型方法。泛型让程序员能够针对泛化的数据类型编写相同的算法，极大增强了编程语言的类型系统和抽象能力。

### （11）Java序列化与反序列化的过程
* （1）将对象实例相关的类元数据输出。
* （2）递归地输出类的超类描述直到不再有超类。
* （3）类元数据完了以后，开始从最顶层的超类开始输出对象实例的实际数据值。
* （4）从上至下递归输出实例的数据

### （12）equals和hashCode方法的关系？
正常情况下二者没啥关系，只有当一个类需要放入依赖hash函数的容器中时，该类必须重写hashCode()和equals()。这两个方法一起被用于查询操作。
强制性关系：如果两个对象equals()为true，则hashCode()结果必然相等。

### （13）说说Java中常见的集合吧
* Collection
  * List
    * ArrayList
    * LinkedList
    * Vecter
  * Set
    * HashSet
    * LinkedHashSet
    * TreeSet
  * Queue
    * PriorityQueue
    * ConcurrentLinkedQueue
* Map
  * HashMap
  * LinkedHashMap
  * HashTable
  * TreeMap
  * ConcurrentHashMap

### （14）HashMap和Hashtable的区别有哪些？
* HashMap没有考虑同步，是线程不安全的；Hashtable使用了synchronized关键字，是线程安全的。
* HashMap允许null作为Key；Hashtable不允许null作为Key，Hashtable的value也不可以为null。
* HashMap初始容量为16，HashTable初始容量为11。
* HashMap实现Map接口，HashTable实现Map和Dictionary接口。
* HashMap链表采用尾插法，HashTable使用头插法。

### （15）HashMap线程不安全体现在哪儿？
HashMap线程不安全主要是考虑到了多线程环境下进行扩容可能会出现HashMap死循环。

### （16）ConcurrentHashMap和Hashtable的区别？
* HashTable使用synchronized方法，每次put、remove时都要锁住整个方法。
* ConcurrentHashMap使用CAS和synchronized块，锁的粒度更加精细。

### （17）HashMap、ConcurrentHashMap和Hashtable关于null的区别
* HashMap允许一个key为null，允许多个value为null。
* HashTable的key、value都不允许为null。
* ConcurrentHashMap的key、value都不允许为null。

### （18）TreeMap有哪些特性？
* 如果Key存入的是字符串等类型，那么会按照字典默认顺序排序
* 如果传入的是自定义引用类型，比如说User，那么该对象必须实现Comparable接口，并且覆盖其compareTo方法。或者在创建TreeMap的时候，我们必须指定使用的比较器。

### （19）ArrayList和LinkedList有哪些区别？
* ArrayList底层使用了动态数组实现，实质上是一个动态数组
* LinkedList底层使用了双向链表实现，可当作堆栈、队列、双端队列使用
* ArrayList在随机存取方面效率高于LinkedList
* LinkedList在节点的增删方面效率高于ArrayList
* ArrayList必须预留一定的空间，当空间不足的时候，会进行扩容操作
* LinkedList的开销是必须存储节点的信息以及节点的指针信息

### （20）LinkedHashMap和LinkedHashSet有了解吗？
* LinkedHashMap可以记录下元素的插入顺序和访问顺序
* LinkedHashMap内部的Entry继承于HashMap.Node，这两个类都实现了Map.Entry<K,V>
* LinkedHashMap的Entry不光有value，next，还有before和after属性，这样通过一个双向链表，保证了各个元素的插入顺序
* 通过构造方法public LinkedHashMap(int initialCapacity,float loadFactor,boolean accessOrder)， accessOrder传入true可以实现LRU缓存算法（访问顺序）
* LinkedHashSet 底层使用LinkedHashMap实现

### （21）什么是LRU算法？LinkedHashMap如何实现LRU算法？
LRU（Least recently used，最近最少使用）算法根据数据的历史访问记录来进行淘汰数据，其核心思想是“如果数据最近被访问过，那么将来被访问的几率也更高”。由于LinkedHashMap可以记录下Map中元素的访问顺序，所以可以轻易的实现LRU算法。只需要将构造方法的accessOrder传入true，并且重写removeEldestEntry方法即可

### （22）Iterator和ListIterator的区别是什么？
* Iterator可以遍历list和set集合；ListIterator只能用来遍历list集合
* Iterator前者只能前向遍历集合；ListIterator可以前向和后向遍历集合
* ListIterator其实就是实现了前者，并且增加了一些新的功能。

### （23）进程与线程的区别：（重点掌握）
* 进程是一个“执行中的程序”，是系统进行资源分配最小单元
* 线程是进程的一个实体，一个进程中一般拥有多个线程，是cpu调度的最小单元。
* 每一个线程都有自己独立的程序计数器、虚拟机栈。
* 线程一般不拥有系统资源，但是也有一些必不可少的资源（使用ThreadLocal存储）
* 线程上下文的切换比进程上下文切换要快很多。

### （24）多线程与单线程的关系：（掌握）
* 多线程是指在一个进程中，并发执行了多个线程，每个线程都实现了不同的功能
* 多线程会存在线程上下文切换，会导致程序执行速度变慢
* 多线程不会提高程序的执行速度，反而会降低速度。但是对于用户来说，可以减少用户的等待响应时间，提高了资源的利用效率

### （25）线程的状态有哪些？（掌握）
* new 新建
* runnable 运行
* terminated 结束
* blocked 阻塞
* waiting 等待
* timed_waiting 限时等待

### （26）多线程编程中常用的函数比较：
* sleep() ：Thread类的静态方法，当前线程将睡眠n毫秒，线程进入阻塞状态。当睡眠时间到了，会解除阻塞，进入可运行状态，等待CPU的到来。睡眠不释放锁（如果有的话）。
* wait() ：是Object的方法，必须与synchronized关键字一起使用，线程进入阻塞状态，当notify或者notifyall被调用后，会解除阻塞。但是，只有重新占用互斥锁之后才会进入可运行状态。睡眠时，会释放互斥锁。
* join() ：当前线程调用，则其它线程全部停止，等待当前线程执行完毕，接着执行。
* yield() ：该方法使得线程放弃当前分得的 CPU 时间。但是不使线程阻塞，即线程仍处于可执行状态，随时可能再次分得 CPU 时间。

### （27）线程活性故障有哪些？
由于资源的稀缺性或者程序自身的问题导致线程一直处于非Runnable状态，并且其处理的任务一直无法完成的现象被称为是线程活性故障。常见的线程活性故障包括死锁，锁死，活锁与线程饥饿。

* 线程死锁：死锁是最常见的一种线程活性故障。死锁的起因是多个线程之间相互等待对方而被永远暂停（处于非Runnable）。死锁的产生必须满足如下四个必要条件：

  * 资源互斥：一个资源每次只能被一个线程使用
  * 请求与保持条件：一个线程因请求资源而阻塞时，对已获得的资源保持不放
  * 不剥夺条件：线程已经获得的资源，在未使用完之前，不能强行剥夺
  * 循环等待条件：若干线程之间形成一种头尾相接的循环等待资源关系

  避免死锁：

  * 粗锁法：使用一个粒度粗的锁来消除“请求与保持条件”，缺点是会明显降低程序的并发性能并且会导致资源的浪费。
  * 锁排序法：指定获取锁的顺序，比如某个线程只有获得A锁和B锁，才能对某资源进行操作

* 线程锁死：指等待线程由于唤醒其所需的条件永远无法成立，或者其他线程无法唤醒这个线程而一直处于非运行状态（线程并未终止）导致其任务 一直无法进展。

  * 信号丢失锁死：信号丢失锁死是因为没有对应的通知线程来将等待线程唤醒，导致等待线程一直处于等待状态。
  * 嵌套监视器锁死：嵌套监视器锁死是由于嵌套锁导致等待线程永远无法被唤醒的一种故障。

* 活锁：活锁是一种特殊的线程活性故障。当一个线程一直处于运行状态，但是其所执行的任务却没有任何进展称为活锁。比如，一个线程一直在申请其所需要的资源，但是却无法申请成功。

* 线程饥饿：线程饥饿是指线程一直无法获得其所需的资源导致任务一直无法运行的情况。线程调度模式有公平调度和非公平调度两种模式。在线程的非公平调度模式下，就可能出现线程饥饿的情况。

### （28）原子性，可见性与有序性：
* 原子性：对于涉及到共享变量访问的操作，若该操作从执行线程以外的任意线程来看是不可分割的，那么该操作就是原子操作，该操作具有原子性。即，其它线程不会“看到”该操作执行了部分的中间结果。
* 可见性：可见性是指一个线程对于共享变量的更新，对于后续访问该变量的线程是立即可见的。
* 有序性是指一个处理器上运行的线程所执行的内存访问操作在另外一个处理器上运行的线程来看是有序的。

### （29）谈谈你对synchronized关键字的理解。
synchronized是Java中的一个关键字，是一个内部锁。它可以使用在方法上和方法块上，表示同步方法和同步代码块。在多线程环境下，同步方法或者同步代码块在同一时刻只允许有一个线程在执行，其余线程都在等待获取锁，也就是实现了整体并发中的局部串行。

monitor锁实现
* 进入时，执行monitorenter，将计数器+1，释放锁monitorexit时，计数器-1
* 当一个线程判断到计数器为0时，则当前锁空闲，可以占用；反之，当前线程进入阻塞状态

### （30）谈谈你对volatile关键字的理解。
volatile关键字是一个轻量级的锁，可以保证可见性和有序性，但是不保证原子性。
* volatile 可以保证主内存和工作内存直接产生交互，进行读写操作，保证可见性
* volatile 仅能保证变量写操作的原子性，不能保证读写操作的原子性。
* volatile可以禁止指令重排序（通过插入内存屏障），典型案例是在单例模式中使用。

### （31）ReentrantLock和synchronized的区别：
* synchronized是Java提供的关键字，使用简单便捷，ReentrantLock是并发包下的同步工具，功能较多。
* synchronized是隐式锁，内部使用monitor锁实现；ReentrantLock是显示锁，内部使用AQS实现。
* synchronized是非公平锁，ReentrantLock可选择公平与非公平。
* 使用synchronized时，线程竞争锁失败进入阻塞队列，此时线程状态为BLOCKED，使用ReentrantLock时，线程竞争锁失败进入等待队列，此时线程状态为WAITING。
* synchronized是一种可升级锁，无锁、偏向锁、轻量级锁、重量级锁。

### （32）Java中的线程池有了解吗？
java.util.concurrent.ThreadPoolExecutor类就是一个线程池。客户端调用ThreadPoolExecutor.submit(Runnable task)提交任务，线程池内部维护的工作者线程的数量就是该线程池的线程池大小，有3种形态：

* 当前线程池大小：表示线程池中实际工作者线程的数量
* 最大线程池大小（maxinumPoolSize）：表示线程池中允许存在的工作者线程的数量上限
* 核心线程大小（corePoolSize ）：表示一个不大于最大线程池大小的工作者线程数量上限

线程池的优势体现如下：

* 线程池可以重复利用已创建的线程，一次创建可以执行多次任务，有效降低线程创建和销毁所造成的资源消耗；
* 线程池技术使得请求可以快速得到响应，节约了创建线程的时间；
* 线程的创建需要占用系统内存，消耗系统资源，使用线程池可以更好的管理线程，做到统一分配、调优和监控线程，提高系统的稳定性。

参数解析
* corePoolSize：核心线程数
* maximumPoolSize：最大线程数
* keepAliveTime ：线程空闲但是保持不被回收的时间
* unit：时间单位
* workQueue：存储线程的队列
* threadFactory：创建线程的工厂
* handler：拒绝策略

线程池的排队策略
* 抛出异常
* 直接丢弃
* 使用调用者线程执行任务
* 移除最老的等待线程

常见的线程池类型：
* newFixedThreadPool(int number) 
  * corePoolSize == maximumPoolSize == number
  * 固定大小的线程池
  * 当线程池大小达到核心线程池大小，就不会增加也不会减小工作者线程的固定大小的线程池
  * 工作队列采用无界队列，理论可以接受2^31个任务

* newSingleThreadExecutor()
  * corePoolSize == maximumPoolSize == 1
  * 其他和newFixedThreadPool一样

* newCachedThreadPool()
  * 工作队列容量为 == 0
  * corePoolSize == 0
  * maximumPoolSize == 2^31
  * keepAliveTime == 60秒
  * 来一个任务时，直接创建一个非核心线程执行，执行完检查队列，如果没有任务，等60秒过后线程销毁。

### （33）ThreadLocal有了解吗？
使用ThreadLocal维护变量时，其为每个使用该变量的线程提供独立的变量副本，所以每一个线程都可以独立的改变自己的副本，而不会影响其他线程对应的副本。
ThreadLocal内部实现机制：

* 每个线程内部都会维护一个类似HashMap的对象，称为ThreadLocalMap，里边会包含若干了Entry（K-V键值对），相应的线程被称为这些Entry的属主线程
* Entry的Key是一个ThreadLocal实例，Value是一个线程特有对象。Entry的作用是为其属主* 线程建立起一个ThreadLocal实例与一个线程特有对象之间的对应关系
Entry对Key的引用是弱引用；Entry对Value的引用是强引用。

### （34）什么是happened-before原则？
对于两个操作A和B，这两个操作可以在不同的线程中执行。如果A Happens-Before B，那么可以保证，当A操作执行完后，A操作的执行结果对B操作是可见的。
* 程序顺序规则：在一个线程内部，按照程序代码的书写顺序，书写在前面的代码操作Happens-Before书写在后面的代码操作。
* 锁定规则：同一时刻只能有一个线程执行锁中的操作，所以锁中的操作被重排序外界是不关心的，只要最终结果能被外界感知到就好。
* volatile变量规则：对一个volatile变量的写操作及这个写操作之前的所有操作Happens-Before对这个变量的读操作及这个读操作之后的所有操作。
* 线程启动规则：Thread对象的start方法及书写在start方法前面的代码操作Happens-Before此线程的每一个动作。
* 线程中的任何操作都Happens-Before其它线程检测到该线程已经结束。这个说法有些抽象，下面举例子对其进行说明。
* 一个线程在另一个线程上调用interrupt,Happens-Before被中断线程检测到interrupt被调用。
* 一个对象的构造函数执行结束Happens-Before它的finalize()方法的开始。

### （35）JVM虚拟机对内部锁有哪些优化？
* 偏向锁

### （36）如何进行无锁化编程？
* CAS

### （37）CAS以及如何解决ABA问题？
* 给对象添加版本号

### （38）JVM中的内存是怎么划分的？（重点掌握）
* 方法区：方法区是一个线程之间共享的区域。常量，静态变量以及JIT编译后的代码都在方法区。主要用于存储已被虚拟机加载的类信息，垃圾回收效果一般，通过-XX：MaxPermSize控制上限。
* 堆内存：堆内存是垃圾回收的主要场所，也是线程之间共享的区域，主要用来存储创建的对象实例，通过-Xmx 和-Xms 可以控制大小。
* 虚拟机栈（栈内存）：栈内存中主要保存局部变量、基本数据类型变量以及堆内存中某个对象的引用变量。每个方法在执行的同时都会创建一个栈帧（Stack Frame）用于存储局部变量表，操作数栈，动态链接，方法出口等信息。栈中的栈帧随着方法的进入和退出有条不紊的执行着出栈和入栈的操作。
* 程序计数器： 程序计数器是当前线程执行的字节码的位置指示器。字节码解释器工作时就是通过改变这个计数器的值来选取下一条需要执行的字节码指令，是内存区域中唯一一个在虚拟机规范中没有规定任何OutOfMemoryError情况的区域。
* 本地方法栈： 主要是为JVM提供使用native 方法的服务。

### （39）类加载过程
* 加载：
  * 通过一个类的全限定名获取此类的二进制流
  * 将这个字节流所代表的静态存储结构转化为方法区的运行时结构
  * 在堆中中生成一个代表这个类的Class对象，作为方法区中类的各种数据的访问入口
* 验证：
  * 确保Class字节流中包含的信息不会危害虚拟机自身的安全
  * 文件格式验证：验证字节流中的内容是否符合Class文件的规范，并能被当前版本虚拟机识别
  * 元数据验证：对字节码描述的信息进行语义分析，保证语义、语法正确。
  * 字节码验证：通过数据流分析和控制流分析，确定语义合法，逻辑正确。
  * 符号引用验证：为确保解析阶段正确执行，检查符号引用对应的信息是否真实有效。
* 准备：
  * 为类变量分配内存并赋予初值（0/null/flase）（final修饰的变量直接赋值），这块内存逻辑上属于方法区，实际上随着Class对象一起存在堆中。
* 解析：
  * 将常量池中的符号引用替换为直接引用
* 初始化：初始化阶段就是执行类构造器cinit()的过程，cinit()是编译器自动生成的方法，它会收集类中所有类变量的赋值动作和静态语句块中的语句合并产生的，收集顺序根据源代码编写顺序决定，静态语句块中只能访问在它之前声明的变量，在它之后的变量只能赋值，不能访问。执行cinit之前先执行父类的cinit方法。

### （40）对象创建过程

一般情况下我们通过new指令来创建对象，当虚拟机遇到一条new指令的时候，会去检查这个指令的参数是否能在常量池中定位到某个类的符号引用，并且检查这个符号引用代表的类是否已经被加载，解析和初始化。如果没有，那么会执行类加载过程。

通过执行类的加载，验证，准备，解析，初始化步骤，完成了类的加载，这个时候会为该对象进行内存分配，也就是把一块确定大小的内存从Java堆中划分出来，在分配的内存上完成对象的创建工作。

对象的内存分配有两种方式，即指针碰撞和空闲列表方式。

指针碰撞方式：

假设Java堆中的内存是绝对规整的，用过的内存在一边，未使用的内存在另一边，中间有一个指示指针，那么所有的内存分配就是把那个指针向空闲空间那边挪动一段与对象大小相等的距离。

空闲列表方式：

如果Java堆内存中不是规整的，已使用和未使用的内存相互交错，那么虚拟机就必须维护一个列表用来记录哪块内存是可用的，在分配的时候找到一块足够大的空间分配对象实例，并且需要更新列表上的记录。

### （41）对象被访问的时候是怎么被找到的？
* 句柄访问方式：
* 直接指针访问方式：（HotSpot）

### （42）root根
* 静态变量或常量
* 虚拟机栈和本地方法栈的引用
* 被锁到的对象
* 虚拟机自带的如类加载器
* 老年区的一部分存在跨代引用的对象

### （43）redis命令
* string：
  * set key value
  * set key value ex 100 （100秒过期）
  * set key value nx （不存在时成功）
  * set key value xx （存在时成功）
  * get key
  * getrange 0 -1
  * getset key newValue （设置新值，返回旧值）
  * strlen key （字符串长度）
  * append key _value （追加字符串）
  * setrange key offset _value （从offset后的字符被替换为_value）
  * incr age （自增一个数字值）
  * incrby age 5 （数字增加一个值）
  * incrbyfloat age 2.3333 （增加一个浮点数）
  * decr age
  * decrby age 5
  * mset key1 value1 key2 value2
  * mget key1 key2
* list:
  * lpush list 1
  * lpush list 2 3 4
  * lpushx list 1 （存在时成功）
  * lpop list
  * rpoplpush source target
  * lindex list 0
  * linsert list 0 value
  * lset list 0 value
  * lrange list 0 -1
  * ltrim list 2 4
  * blpop list
  * brpop list
  * brpoplpush source target
* hash:
  * hset key field value
  * hsetnx key field value
  * hget key field
  * hexists key field
  * hdel key field
  * hlen key
  * hstrlen key field
  * hincrby key field 5
  * hincrbyfloat key field 2.333
  * hmset key field1 value1 field2 value2
  * hmget key field1 field2
  * hkeys key
  * hvals key
  * hgetall key
* set:
  * sadd key 1
  * sismember key member
  * spop key （随机移除集合中的一个成员）
  * srandmember key （随机选择一个成员）
  * srem key member
  * smove source target member
  * scard key
  * smembers key
  * sinter key1 key2 key3 （返回交集）
  * sinterstore key1 key2 key3 target（返回交集，输入到target）
  * sunion key1 key2 key3 （返回并集）
  * sunionstore key1 key2 key3 target
  * sdiff key1 key2 （返回差集）
  * sdiffstore key1 key2
* zset:
  * zadd key score member
  * zscore key member
  * zincrby key 5 member
  * zcard key
  * zcount key min max
  * zrange key 0 -1
  * zrevrange key 0 -1
  * zrangebyscore key min max
  * zrevrangebyscore key min max
  * zrank key member
  * zrevrank key member
  * zrem key member
  * zremrangebyrank key start end
  * zremrangebyscore key min max
  * zunionstore target numkeys key1 key2 key3
  * 
