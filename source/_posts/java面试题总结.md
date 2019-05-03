---
title: java面试题总结.md
date: 2019-02-27 09:41:47
tags: [java,面试]
password: 
categories: java基础-面试
---
[参考链接①](https://www.cnblogs.com/xdp-gacl/p/3641769.html)
[参考链接②](https://www.jianshu.com/p/c01eb6e46226)
---
# java基础部分：

## 一、数据类型：
### 1、String 是最基本的数据类型吗？
    不是。Java中的基本数据类型只有8个：
    byte、short、int、long、float、double、char、boolean；
    除了基本类型（primitive type），剩下的都是引用类型（reference type），
    Java 5以后引入的枚举类型也算是一种比较特殊的引用类型。
    
    
### 2、float f=3.4;是否正确？   
    不正确。3.4是双精度数，将双精度型（double）赋值给浮点型（float）
    属于下转型（down-casting，也称为窄化）会造成精度损失，
    因此需要强制类型转换float f =(float)3.4; 
              或者写成float f =3.4F; 
  
  
### 3、short s1 = 1; s1 = s1 + 1;有什么错? short s1 = 1; s1 += 1;有什么错?
    对于short s1 = 1; s1 = s1 + 1; 由于s1+1运算时会自动提升表达式的类型，
    所以结果是int型，再赋值给short类型s1时，编译器将报告需要强制转换类型的错误。
    
    对于short s1 = 1; s1 += 1;由于 += 是java语言规定的运算符，
    java编译器会对它进行特殊处理，因此可以正确编译。 
    
    
### 4、char型变量中能不能存贮一个中文汉字?为什么?
    在switch（expr1）中，expr1只能是一个整数表达式或者枚举常量，
    整数表达式可以是int基本类型或Integer包装类型，
    由于，byte,short,char都可以隐含转换为int，所以，这些类型以及这些类型的包装类型也是可以的。
    显然，long和String类型都不符合switch的语法规定，并且不能被隐式转换成int类型，
    所以，它们不能作用于swtich语句中。 
    

### 5、Integer与int的区别
    int是java提供的8种原始数据类型之一。Java为每个原始类型提供了封装类，
    Integer是java为int提供的封装类。int的默认值为0，而Integer的默认值为null，
    即Integer可以区分出未赋值和值为0的区别，int则无法表达出未赋值的情况，
    例如，要想表达出没有参加考试和考试成绩为0的区别，则只能使用Integer。
    在JSP开发中，Integer的默认为null，所以用el表达式在文本框中显示时，
    值为空白字符串，而int默认的默认值为0，所以用el表达式在文本框中显示时，结果为0，
    所以，int不适合作为web层的表单数据的类型。


### 6、switch 是否能作用在byte 上，是否能作用在long 上，是否能作用在String上？
    在Java 5以前，switch(expr)中，expr只能是byte、short、char、int。
    从Java 5开始，Java中引入了枚举类型，expr也可以是enum类型，从Java 7开始，
    expr还可以是字符串（String），但是长整型（long）在目前所有的版本中都是不可以的。
    
    
### 7、数组有没有length()方法？String有没有length()方法？
    数组没有length()方法，有length 的属性。String 有length()方法。JavaScript中，
    获得字符串的长度是通过length属性得到的，这一点容易和Java混淆。
    
    
### 8、String和StringBuilder、StringBuffer的区别？
    Java平台提供了两种类型的字符串：String和StringBuffer/StringBuilder，
    它们可以储存和操作字符串。其中String是只读字符串，
    也就意味着String引用的字符串内容是不能被改变的。
    而StringBuffer/StringBuilder类表示的字符串对象可以直接进行修改。
    StringBuilder是Java 5中引入的，它和StringBuffer的方法完全相同，
    区别在于它是在单线程环境下使用的，因为它的所有方面都没有被synchronized修饰，
    因此它的效率也比StringBuffer要高。
    

### 9、
    

## 二、关键字：

### 1、访问修饰符public,private,protected,以及不写（默认）时的区别？
!(kk)[访问修饰符.jpg]


### 2、Java 中的final关键字有哪些用法？
    (1)修饰类：表示该类不能被继承；
    (2)修饰方法：表示方法不能被重写；
    (3)修饰变量：表示变量只能一次赋值以后值不能被修改（常量）。
    
    
### 3、Java语言如何进行异常处理，关键字：throws、throw、try、catch、finally分别如何使用？
    Java通过面向对象的方法进行异常处理，把各种不同的异常进行分类，并提供了良好的接口。
    在Java中，每个异常都是一个对象，它是Throwable类或其子类的实例。
    当一个方法出现异常后便抛出一个异常对象，该对象中包含有异常信息，
    调用这个对象的方法可以捕获到这个异常并可以对其进行处理。
    Java的异常处理是通过5个关键词来实现的：try、catch、throw、throws和finally。
    一般情况下是用try来执行一段程序，如果系统会抛出（throw）一个异常对象，
    可以通过它的类型来捕获（catch）它，或通过总是执行代码块（finally）来处理；
    try用来指定一块预防所有异常的程序；
    catch子句紧跟在try块后面，用来指定你想要捕获的异常的类型；
    throw语句用来明确地抛出一个异常；
    throws用来声明一个方法可能抛出的各种异常（当然声明异常时允许无病呻吟）；
    finally为确保一段代码不管发生什么异常状况都要被执行；
    try语句可以嵌套，每当遇到一个try语句，异常的结构就会被放入异常栈中，
    直到所有的try语句都完成。如果下一级的try语句没有对某种异常进行处理，
    异常栈就会执行出栈操作，直到遇到有处理这种异常的try语句或者最终将异常抛给JVM。
    
    
### 4、阐述final、finally、finalize的区别。
final：修饰符（关键字）有三种用法：
```
    (1)如果一个类被声明为final，意味着它不能再派生出新的子类，
    即不能被继承，因此它和abstract是反义词。
    (2)将变量声明为final，可以保证它们在使用中不被改变，
        被声明为final的变量必须在声明时给定初值，而在以后的引用中只能读取不可修改
        （如果修饰引用，那么表示引用不可变，引用指向的内容可变）。
    (3)被声明为final的方法也同样只能使用，不能在子类中被重写。
    (4)被final修饰的方法，JVM会尝试将其内联，以提高运行效率 
    (5)被final修饰的常量，在编译阶段会存入常量池中。
    回答出编译器对final域要遵守的两个重排序规则更好：
    1.在构造函数内对一个final域的写入，与随后把这个被构造对象的引用赋值给一个引用变量,
        这两个操作之间不能重排序。
    2.初次读一个包含final域的对象的引用，与随后初次读这个final域,
        这两个操作之间不能重排序。
```
finally：

    通常放在try…catch…的后面构造总是执行代码块，这就意味着程序无论正常执行还是发生异常，
    这里的代码只要JVM不关闭都能执行，可以将释放外部资源的代码写在finally块中。
    
finalize：

    Object类中定义的方法，Java中允许使用finalize()方法在垃圾收集器将对象
    从内存中清除出去之前做必要的清理工作。这个方法是由垃圾收集器在销毁对象时调用的，
    通过重写finalize()方法可以整理系统资源或者执行其他清理工作。
    

### 5、
    
    

## 三、集合（java容器）数据结构和运算：

### 1、用最有效率的方法计算2乘以8？
    2 << 3（左移3位相当于乘以2的3次方，右移3位相当于除以2的3次方）。
    
    
### 2、计算一个数的质因数，例如：输入10，输出 10=1*2*5
```
    System.out.println("请输入一个数!");
    Scanner sc = new Scanner(System.in);
    int num = Integer.parseInt(sc.next());
    String str = num+"=1";
    while(num != 1){
        for(int i = 2;i<=num;i++){
            if(num%i==0){
                str = str +"*"+i;
                System.out.println(i);
                num = num/i;
                break;
            }
        }
    }
    System.out.println(str);
```    


### 3、&和&&的区别？
    &运算符有两种用法：(1)按位与；(2)逻辑与。&&运算符是短路与运算。
    逻辑与跟短路与的差别是非常巨大的，虽然二者都要求运算符左右两端的布尔值都是true
    整个表达式的值才是true。&&之所以称为短路运算是因为，如果&&左边的表达式的值是false，
    右边的表达式会被直接短路掉，不会进行运算。很多时候我们可能都需要用&&而不是&，
    例如在验证用户登录时判定用户名不是null而且不是空字符串，
    应当写为：username != null &&!username.equals("")，二者的顺序不能交换，
    更不能用&运算符，因为第一个条件如果不成立，根本不能进行字符串的equals比较，
    否则会产生NullPointerException异常。
    注意：逻辑或运算符（|）和短路或运算符（||）的差别也是如此。
    

### 4、在Java中，如何跳出当前的多重嵌套循环？
    在最外层循环前加一个标记如A，然后用break A;
    可以跳出多重循环。（Java中支持带标签的break和continue语句，
    作用有点类似于C和C++中的goto语句，但是就像要避免使用goto一样，
    应该避免使用带标签的break和continue，因为它不会让你的程序变得更优雅，
    很多时候甚至有相反的作用，所以这种语法其实不知道更好）
    
  
### 5、List、Set、Map是否继承自Collection接口？
    List、Set 是，Map 不是。Map是键值对映射容器，与List和Set有明显的区别，
    而Set存储的零散的元素且不允许有重复元素（数学中的集合也是如此），
    List是线性结构的容器，适用于按数值索引访问元素的情形。
    
    
### 6、阐述ArrayList、Vector、LinkedList的存储性能和特性。
    ArrayList 和Vector都是使用数组方式存储数据，
    此数组元素数大于实际存储的数据以便增加和插入元素，它们都允许直接按序号索引元素，
    但是插入元素要涉及数组元素移动等内存操作，所以索引数据快而插入数据慢，
    Vector中的方法由于添加了synchronized修饰，因此Vector是线程安全的容器，
    但性能上较ArrayList差，因此已经是Java中的遗留容器。
    LinkedList使用双向链表实现存储（将内存中零散的内存单元通过附加的引用关联起来，
    形成一个可以按序号索引的线性结构，这种链式存储方式与数组的连续存储方式相比，
    内存的利用率更高），按序号索引数据需要进行前向或后向遍历，
    但是插入数据时只需要记录本项的前后项即可，所以插入速度较快。
    Vector属于遗留容器（Java早期的版本中提供的容器，除此之外，
    Hashtable、Dictionary、BitSet、Stack、Properties都是遗留容器），
    已经不推荐使用，但是由于ArrayList和LinkedListed都是非线程安全的，
    如果遇到多个线程操作同一个容器的场景，
    则可以通过工具类Collections中的synchronizedList方法将其转换成
    线程安全的容器后再使用（这是对装潢模式的应用，将已有对象传入另一个类的
    构造器中创建新的对象来增强实现）。
```
补充：遗留容器中的Properties类和Stack类在设计上有严重的问题，
Properties是一个键和值都是字符串的特殊的键值对映射，
在设计上应该是关联一个Hashtable并将其两个泛型参数设置为String类型，
但是Java API中的Properties直接继承了Hashtable，这很明显是对继承的滥用。
这里复用代码的方式应该是Has-A关系而不是Is-A关系，另一方面容器都属于工具类，
继承工具类本身就是一个错误的做法，使用工具类最好的方式是Has-A关系（关联）
或Use-A关系（依赖）。同理，Stack类继承Vector也是不正确的。
Sun公司的工程师们也会犯这种低级错误，让人唏嘘不已。

```


### 7、Collection和Collections的区别？
    Collection是一个接口，它是Set、List等容器的父接口；
    Collections是个一个工具类，提供了一系列的静态方法来辅助容器操作，
    这些方法包括对容器的搜索、排序、线程安全化等等。
    
    
### 8、List、Map、Set三个接口存取元素时，各有什么特点？
    List以特定索引来存取元素，可以有重复元素。
    Set不能存放重复元素（用对象的equals()方法来区分元素是否重复）。
    Map保存键值对（key-value pair）映射，映射关系可以是一对一或多对一。
    Set和Map容器都有基于哈希存储和排序树的两种实现版本，
    基于哈希存储的版本理论存取时间复杂度为O(1)，
    而基于排序树版本的实现在插入或删除元素时会按照元素或元素的键（key）
    构成排序树从而达到排序和去重的效果。
    
    
### 9、 "=="和equals方法究竟有什么区别？
    “==”操作符专门用来比较两个变量的值是否相等，也就是用于比较变量所对应的内存中所存储的数值是否相同，
    要比较两个基本类型的数据或两个引用变量是否相等，只能用==操作符。
    
    　　如果一个变量指向的数据是对象类型的，那么，这时候涉及了两块内存，
    对象本身占用一块内存（堆内存），变量也占用一块内存(栈内存)，
    例如Objet obj = new Object();变量obj是一个内存，new Object()是另一个内存，
    此时，变量obj所对应的内存中存储的数值就是对象占用的那块内存的首地址。
    对于指向对象类型的变量，如果要比较两个变量是否指向同一个对象，
    即要看这两个变量所对应的内存中的数值是否相等，这时候就需要用==操作符进行比较。
    
    　　equals方法是用于比较两个独立对象的内容是否相同，
    就好比去比较两个人的长相是否相同，它比较的两个对象是独立的。
    例如，对于下面的代码：
```
    　　String a=new String("foo");
    
    　　String b=new String("foo");
```
    
    　　两条new语句创建了两个对象，然后用a,b这两个变量分别指向了其中一个对象，
    这是两个不同的对象，它们的首地址是不同的，即a和b中存储的数值是不相同的，
    所以，表达式a==b将返回false，而这两个对象中的内容是相同的，所以，
    表达式a.equals(b)将返回true。
    
    　　在实际开发中，我们经常要比较传递进行来的字符串内容是否等，
    例如，String input = …;input.equals(“quit”)，许多人稍不注意就使用==进行比较了，
    这是错误的，记住，字符串的比较基本上都是使用equals方法。
    
    　　如果一个类没有自己定义equals方法，那么它将继承Object类的equals方法，
    Object类的equals方法的实现代码如下：
```
boolean equals(Object o){
    return this==o;
}
```
    　　这说明，如果一个类没有自己定义equals方法，它默认的equals方法（从Object 类继承的）
    就是使用==操作符，也是在比较两个变量指向的对象是否是同一对象，
    这时候使用equals和使用==会得到同样的结果，如果比较的是两个独立的对象则总返回false。
    如果你编写的类希望能够比较该类创建的两个实例对象的内容是否相同，
    那么你必须覆盖equals方法，由你自己写代码来决定在什么情况即可认为两个对象的内容是相同的。
    


### 10、java 中的 Math常用方法？
    常用值与函数：

    Math.PI 记录的圆周率 
    Math.E 记录e的常量 
    Math中还有一些类似的常量，都是一些工程数学常用量。
    
    Math.abs 求绝对值 
    Math.sin 正弦函数 Math.asin 反正弦函数 
    Math.cos 余弦函数 Math.acos 反余弦函数 
    Math.tan 正切函数 Math.atan 反正切函数 Math.atan2 商的反正切函数 
    Math.toDegrees 弧度转化为角度 Math.toRadians 角度转化为弧度 
    Math.ceil 得到不小于某数的最大整数 
    Math.floor 得到不大于某数的最大整数 
    Math.IEEEremainder 求余 
    Math.max 求两数中最大 
    Math.min 求两数中最小 
    Math.sqrt 求开方 
    Math.pow 求某数的任意次方, 抛出ArithmeticException处理溢出异常 
    Math.exp 求e的任意次方 
    Math.log10 以10为底的对数 
    Math.log 自然对数 
    Math.rint 求距离某数最近的整数（可能比某数大，也可能比它小） 
    Math.round 同上，返回int型或者long型（上一个函数返回double型） 
    Math.random 返回0，1之间的一个随机数
    
    
### 11、位运算
    <<:左移运算符
    （左移位运算符（<<）能将运算符左边的运算对象向左移动运算符右侧指定的位数（在低位补0））
    例子：a<<b   相当于a乘以2的b次冥
    
    >>:右移运算符
    （“有符号”右移位运算符（>>）则将运算符左边的运算对象向右移动运算符右侧指定的位数。 
    “有符号”右移位运算符使用了“符号扩展”：若值为正，则在高位插入0；若值为负，则在高位插入1）
    例子：a>>b   相当于a除以2的b次冥
    
    >>>：无符号右移，忽略符号位，空位都以0补齐
    （“无符号”右移位运算符（>>>），它使用了“零扩展”：无论正负，都在高位插入0）
    
    ^:按位异或可以用来使某些特定的位翻转，
    如对数10100001的第2位和第3位翻转，可以将数与00000110进行按位异或运算。 　
    10100001^00000110=10100111 //1010 0001 ^ 0x06 = 1010 0001 ^ 6 
    通过按位异或运算，可以实现两个值的交换，而不必使用临时变量。
    例如交换两个整数a，b的值，可通过下列语句实现：
     a=10100001,b=00000110 
     a=a^b； 　　//a=10100111 
     b=b^a； 　　//b=10100001
     a=a^b； 　　//a=00000110
     异或运算符的特点是：数a两次异或同一个数b（a=a^b^b）仍然为原值a.
     
     &:与运算符用符号“&”表示，其使用规律如下：
        两个操作数中位都为1，结果才为1，否则结果为0。
     
     |:或运算符用符号“|”表示，其运算规律如下：
        两个位只要有一个为1，那么结果就是1，否则就为0。
     
     ~:非运算符用符号“~”表示，其运算规律如下：
        如果位为0，结果是1，如果位为1，结果是0。
        
     ^:异或运算符是用符号“^”表示的，其运算规律是：
        两个操作数的位中，相同则结果为0，不同则结果为1。
   
        
### 12、
    
## 四、多线程


### 1、面向对象的特征有哪些方面？
    抽象：将同类对象的共同特征提取出来构造类。
    继承：基于基类创建新类。
    封装：将数据隐藏起来，对数据的访问只能通过特定接口。
    多态性：不同子类型对象对相同消息作出不同响应。
    
 
### 2、Thread类的sleep()方法和对象的wait()方法都可以让线程暂停执行，它们有什么区别?
    sleep()方法（休眠）是线程类（Thread）的静态方法，
    调用此方法会让当前线程暂停执行指定的时间，将执行机会（CPU）让给其他线程，
    但是对象的锁依然保持，因此休眠时间结束后会自动恢复
    （线程回到就绪状态，请参考第66题中的线程状态转换图）。
    wait()是Object类的方法，调用对象的wait()方法导致当前线程放弃对象的锁（线程暂停执行），
    进入对象的等待池（wait pool），只有调用对象的notify()方法（或notifyAll()方法）
    时才能唤醒等待池中的线程进入等锁池（lock pool），
    如果线程重新获得对象的锁就可以进入就绪状态。
    
```
补充：可能不少人对什么是进程，什么是线程还比较模糊，对于为什么需要多线程编程也不是特别理解。
简单的说：进程是具有一定独立功能的程序关于某个数据集合上的一次运行活动，
是操作系统进行资源分配和调度的一个独立单位；线程是进程的一个实体，
是CPU调度和分派的基本单位，是比进程更小的能独立运行的基本单位。
线程的划分尺度小于进程，这使得多线程程序的并发性高；
进程在执行时通常拥有独立的内存单元，而线程之间可以共享内存。
使用多线程的编程通常能够带来更好的性能和用户体验，但是多线程的程序对于其他程序是不友好的，
因为它可能占用了更多的CPU资源。当然，也不是线程越多，程序的性能就越好，
因为线程之间的调度和切换也会浪费CPU时间。时下很时髦的Node.js就采用了单线程异步I/O的工作模式。
```


### 3、线程的sleep()方法和yield()方法有什么区别？
    ① sleep()方法给其他线程运行机会时不考虑线程的优先级，
        因此会给低优先级的线程以运行的机会；
        yield()方法只会给相同优先级或更高优先级的线程以运行的机会；
    ② 线程执行sleep()方法后转入阻塞（blocked）状态，而执行yield()方法后转入就绪（ready）状态；
    ③ sleep()方法声明抛出InterruptedException，而yield()方法没有声明任何异常；
    ④ sleep()方法比yield()方法（跟操作系统CPU调度相关）具有更好的可移植性。
    

### 4、当一个线程进入一个对象的synchronized方法A之后，其它线程是否可进入此对象的synchronized方法B？
    不能。其它线程只能访问该对象的非同步方法，同步方法则不能进入。
    因为非静态方法上的synchronized修饰符要求执行方法时要获得对象的锁，
    如果已经进入A方法说明对象锁已经被取走，那么试图进入B方法的线程就只能
    在等锁池（注意不是等待池哦）中等待对象的锁。   
 
 
### 5、请说出与线程同步以及线程调度相关的方法。
    wait()：使一个线程处于等待（阻塞）状态，并且释放所持有的对象的锁；
    sleep()：使一个正在运行的线程处于睡眠状态，是一个静态方法，
        调用此方法要处理InterruptedException异常；
    notify()：唤醒一个处于等待状态的线程，当然在调用此方法的时候，
        并不能确切的唤醒某一个等待状态的线程，而是由JVM确定唤醒哪个线程，而且与优先级无关；
    notityAll()：唤醒所有处于等待状态的线程，该方法并不是将对象的锁给所有线程，
        而是让它们竞争，只有获得锁的线程才能进入就绪状态；
```
补充：Java 5通过Lock接口提供了显式的锁机制（explicit lock），
增强了灵活性以及对线程的协调。Lock接口中定义了加锁（lock()）和解锁（unlock()）的方法，
同时还提供了newCondition()方法来产生用于线程之间通信的Condition对象；
此外，Java 5还提供了信号量机制（semaphore），信号量可以用来限制对
某个共享资源进行访问的线程的数量。在对资源进行访问之前，
线程必须得到信号量的许可（调用Semaphore对象的acquire()方法）；
在完成对资源的访问后，线程必须向信号量归还许可（调用Semaphore对象的release()方法）。
```

下面的例子演示了100个线程同时向一个银行账户中存入1元钱，在没有使用同步机制和
使用同步机制情况下的执行情况。
银行账户类：
```
/**
 * 银行账户
 * @author nnngu
 *
 */
public class Account {
    private double balance;     // 账户余额

    /**
     * 存款
     * @param money 存入金额
     */
    public void deposit(double money) {
        double newBalance = balance + money;
        try {
            Thread.sleep(10);   // 模拟此业务需要一段处理时间
        }
        catch(InterruptedException ex) {
            ex.printStackTrace();
        }
        balance = newBalance;
    }

    /**
     * 获得账户余额
     */
    public double getBalance() {
        return balance;
    }
}
```
存钱线程类：
```
/**
 * 存钱线程
 * @author nnngu
 *
 */
public class AddMoneyThread implements Runnable {
    private Account account;    // 存入账户
    private double money;       // 存入金额

    public AddMoneyThread(Account account, double money) {
        this.account = account;
        this.money = money;
    }

    @Override
    public void run() {
        account.deposit(money);
    }

}
```
测试类：
```
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class Test01 {

    public static void main(String[] args) {
        Account account = new Account();
        ExecutorService service = Executors.newFixedThreadPool(100);

        for(int i = 1; i <= 100; i++) {
            service.execute(new AddMoneyThread(account, 1));
        }

        service.shutdown();

        while(!service.isTerminated()) {}

        System.out.println("账户余额: " + account.getBalance());
    }
}
```
在没有同步的情况下，执行结果通常是显示账户余额在10元以下，出现这种状况的原因是，
当一个线程A试图存入1元的时候，另外一个线程B也能够进入存款的方法中，
线程B读取到的账户余额仍然是线程A存入1元钱之前的账户余额，
因此也是在原来的余额0上面做了加1元的操作，同理线程C也会做类似的事情，
所以最后100个线程执行结束时，本来期望账户余额为100元，
但实际得到的通常在10元以下（很可能是1元哦）。解决这个问题的办法就是同步，
当一个线程对银行账户存钱时，需要将此账户锁定，待其操作完成后才允许其他的线程进行操作，
代码有如下几种调整方案：
在银行账户的存款（deposit）方法上加同步（synchronized）关键字
```
/**
 * 银行账户
 * @author nnngu
 *
 */
public class Account {
    private double balance;     // 账户余额

    /**
     * 存款
     * @param money 存入金额
     */
    public synchronized void deposit(double money) {
        double newBalance = balance + money;
        try {
            Thread.sleep(10);   // 模拟此业务需要一段处理时间
        }
        catch(InterruptedException ex) {
            ex.printStackTrace();
        }
        balance = newBalance;
    }

    /**
     * 获得账户余额
     */
    public double getBalance() {
        return balance;
    }
}
```
在线程调用存款方法时对银行账户进行同步
```
/**
 * 存钱线程
 * @author nnngu
 *
 */
public class AddMoneyThread implements Runnable {
    private Account account;    // 存入账户
    private double money;       // 存入金额

    public AddMoneyThread(Account account, double money) {
        this.account = account;
        this.money = money;
    }

    @Override
    public void run() {
        synchronized (account) {
            account.deposit(money); 
        }
    }

}
```
通过Java 5显示的锁机制，为每个银行账户创建一个锁对象，在存款操作进行加锁和解锁的操作
```
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

/**
 * 银行账户
 * 
 * @author nnngu
 *
 */
public class Account {
    private Lock accountLock = new ReentrantLock();
    private double balance; // 账户余额

    /**
     * 存款
     * 
     * @param money
     *            存入金额
     */
    public void deposit(double money) {
        accountLock.lock();
        try {
            double newBalance = balance + money;
            try {
                Thread.sleep(10); // 模拟此业务需要一段处理时间
            }
            catch (InterruptedException ex) {
                ex.printStackTrace();
            }
            balance = newBalance;
        }
        finally {
            accountLock.unlock();
        }
    }

    /**
     * 获得账户余额
     */
    public double getBalance() {
        return balance;
    }
}
```
按照上述三种方式对代码进行修改后，重写执行测试代码Test01，将看到最终的账户余额为100元。
当然也可以使用Semaphore或CountdownLatch来实现同步。


### 6、编写多线程程序有几种实现方式？
    Java 5以前实现多线程有两种实现方法：
    一种是继承Thread类；
    另一种是实现Runnable接口。
    两种方式都要通过重写run()方法来定义线程的行为，推荐使用后者，
    因为Java中的继承是单继承，一个类有一个父类，如果继承了Thread类就无法再继承其他类了，
    显然使用Runnable接口更为灵活。
补充：Java 5以后创建线程还有第三种方式：实现Callable接口，
    该接口中的call方法可以在线程执行结束时产生一个返回值，代码如下所示：
```
import java.util.ArrayList;
import java.util.List;
import java.util.concurrent.Callable;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;


class MyTask implements Callable<Integer> {
    private int upperBounds;

    public MyTask(int upperBounds) {
        this.upperBounds = upperBounds;
    }

    @Override
    public Integer call() throws Exception {
        int sum = 0; 
        for(int i = 1; i <= upperBounds; i++) {
            sum += i;
        }
        return sum;
    }

}

class Test {

    public static void main(String[] args) throws Exception {
        List<Future<Integer>> list = new ArrayList<>();
        ExecutorService service = Executors.newFixedThreadPool(10);
        for(int i = 0; i < 10; i++) {
            list.add(service.submit(new MyTask((int) (Math.random() * 100))));
        }

        int sum = 0;
        for(Future<Integer> future : list) {
            // while(!future.isDone()) ;
            sum += future.get();
        }

        System.out.println(sum);
    }
}
```
    
    
### 7、synchronized关键字的用法？
    synchronized关键字可以将对象或者方法标记为同步，以实现对对象和方法的互斥访问，
    可以用synchronized(对象) { … }定义同步代码块，
    或者在声明方法时将synchronized作为方法的修饰符。
    
    
### 8、举例说明同步和异步。
    如果系统中存在临界资源（资源数量少于竞争资源的线程数量的资源），
    例如正在写的数据以后可能被另一个线程读到，或者正在读的数据可能已经被另一个线程写过了，
    那么这些数据就必须进行同步存取（数据库操作中的排他锁就是最好的例子）。
    当应用程序在对象上调用了一个需要花费很长时间来执行的方法，
    并且不希望让程序等待方法的返回时，就应该使用异步编程，
    在很多情况下采用异步途径往往更有效率。事实上，所谓的同步就是指阻塞式操作，
    而异步就是非阻塞式操作。
    
    
### 9、什么是线程池（thread pool）？
    在面向对象编程中，创建和销毁对象是很费时间的，因为创建一个对象要获取内存资源
    或者其它更多资源。在Java中更是如此，虚拟机将试图跟踪每一个对象，
    以便能够在对象销毁后进行垃圾回收。所以提高服务程序效率的一个手段就是尽可能
    减少创建和销毁对象的次数，特别是一些很耗资源的对象创建和销毁，
    这就是”池化资源”技术产生的原因。线程池顾名思义就是事先创建若干个可执行的线程
    放入一个池（容器）中，需要的时候从池中获取线程不用自行创建，使用完毕不需要
    销毁线程而是放回池中，从而减少创建和销毁线程对象的开销。
    Java 5+中的Executor接口定义一个执行线程的工具。
    它的子类型即线程池接口是ExecutorService。要配置一个线程池是比较复杂的，
    尤其是对于线程池的原理不是很清楚的情况下，因此在工具类Executors里面提供了一些
    静态工厂方法，生成一些常用的线程池，如下所示：
    
    newSingleThreadExecutor：创建一个单线程的线程池。这个线程池只有一个线程在工作，
        也就是相当于单线程串行执行所有任务。如果这个唯一的线程因为异常结束，
        那么会有一个新的线程来替代它。此线程池保证所有任务的执行顺序按照任务的提交顺序执行。
    newFixedThreadPool：创建固定大小的线程池。每次提交一个任务就创建一个线程，
        直到线程达到线程池的最大大小。线程池的大小一旦达到最大值就会保持不变，
        如果某个线程因为执行异常而结束，那么线程池会补充一个新线程。
    newCachedThreadPool：创建一个可缓存的线程池。如果线程池的大小超过了处理任务
        所需要的线程，那么就会回收部分空闲（60秒不执行任务）的线程，当任务数增加时，
        此线程池又可以智能的添加新线程来处理任务。此线程池不会对线程池大小做限制，
        线程池大小完全依赖于操作系统（或者说JVM）能够创建的最大线程大小。
    newScheduledThreadPool：创建一个大小无限的线程池。此线程池支持定时以及
        周期性执行任务的需求。
    
    
### 10、简述synchronized 和java.util.concurrent.locks.Lock的异同？
    Lock是Java 5以后引入的新的API，和关键字synchronized相比主要相同点：
    Lock 能完成synchronized所实现的所有功能；
    主要不同点：Lock有比synchronized更精确的线程语义和更好的性能，
        而且不强制性的要求一定要获得锁。synchronized会自动释放锁，
        而Lock一定要求程序员手工释放，并且最好在finally 块中释放（这是释放外
        部资源的最好的地方）。
   

### 11、 Java中实现线程阻塞的方法?
阻塞指的是暂停一个线程的执行以等待某个条件发生（如某资源就绪）

```
（1）线程睡眠：Thread.sleep (long millis)方法，使线程转到阻塞状态。
    millis参数设定睡眠的时间，以毫秒为单位。当睡眠结束后，就转为就绪（Runnable）状态。
    sleep()平台移植性好。

（2）线程等待：Object类中的wait()方法，导致当前的线程等待，
    直到其他线程调用此对象的 notify() 唤醒方法。这个两个唤醒方法也是Object类中的方法，
    行为等价于调用 wait() 一样。wait() 和 notify() 方法：两个方法配套使用，wait() 
    使得线程进入阻塞状态，它有两种形式，一种允许 指定以毫秒为单位的一段时间作为参数，
    另一种没有参数，前者当对应的 notify() 被调用或者超出指定时间时线程重新进入可执行状态，
    后者则必须对应的 notify() 被调用.

（3）线程礼让，Thread.yield() 方法，暂停当前正在执行的线程对象，
    把执行机会让给相同或者更高优先级的线程。yield() 使得线程放弃当前分得的 CPU 时间，
    但是不使线程阻塞，即线程仍处于可执行状态，随时可能再次分得 CPU 时间。
    调用 yield() 的效果等价于调度程序认为该线程已执行了足够的时间从而转到另一个线程.

（4）线程自闭，join()方法，等待其他线程终止。在当前线程中调用另一个线程的join()方法，
    则当前线程转入阻塞状态，直到另一个进程运行结束，当前线程再由阻塞转为就绪状态。

（5）suspend() 和 resume() 方法：两个方法配套使用，suspend()使得线程进入阻塞状态，
    并且不会自动恢复，必须其对应的resume() 被调用，才能使得线程重新进入可执行状态。
    典型地，suspend() 和 resume() 被用在等待另一个线程产生的结果的情形：
    测试发现结果还没有产生后，让线程阻塞，另一个线程产生了结果后，调用 resume() 
    使其恢复。Thread中suspend()和resume()两个方法在JDK1.5中已经废除，不再介绍。
    因为有死锁倾向。
```  


### 12、Thread类常用方法：
    
    sleep(): 强迫一个线程睡眠Ｎ毫秒。
    
    isAlive(): 判断一个线程是否存活。
    
    join(): 等待线程终止。
    
    activeCount(): 程序中活跃的线程数。
    
    enumerate(): 枚举程序中的线程。
    
    currentThread(): 得到当前线程。
    
    isDaemon(): 一个线程是否为守护线程。
    
    setDaemon(): 设置一个线程为守护线程。(用户线程和守护线程的区别在于，是否等待主线程依赖于主线程结束而结束)
    
    setName(): 为线程设置一个名称。
    
    wait(): 强迫一个线程等待。
    
    notify(): 通知一个线程继续运行。
    
    setPriority(): 设置一个线程的优先级。
    
可以参考下面这篇文章    
[Java线程阻塞方法sleep()和wait()精炼详解](https://blog.csdn.net/weixin_41101173/article/details/79889464)

wait()方法和notify()/notifyAll()方法在调用前都必须先获得对象的锁

    
### 13、产生死锁的条件
    1.互斥条件：一个资源每次只能被一个进程使用。 
    2.请求与保持条件：一个进程因请求资源而阻塞时，对已获得的资源保持不放。 
    3.不剥夺条件:进程已获得的资源，在末使用完之前，不能强行剥夺。 
    4.循环等待条件:若干进程之间形成一种头尾相接的循环等待资源关系。
    
    
### 14、为什么wait, nofity和nofityAll这些方法不放在Thread类当中
    一个很明显的原因是JAVA提供的锁是对象级的而不是线程级的，每个对象都有锁，通过线程获得。
    如果线程需要等待某些锁那么调用对象中的wait()方法就有意义了。
    如果wait()方法定义在Thread类中，线程正在等待的是哪个锁就不明显了。
    简单的说，由于wait，notify和notifyAll都是锁级别的操作，
    所以把他们定义在Object类中因为锁属于对象。


### 15、什么是多线程的上下文切换
       多线程的上下文切换是指CPU控制权由一个已经正在运行的线程切换到另外一个就绪并等待获取CPU执行权的线程的过程。


### 16、synchronized和ReentrantLock的区别
    synchronized是和if、else、for、while一样的关键字，ReentrantLock是类，这是二者的本质区别。
    既然ReentrantLock是类，那么它就提供了比synchronized更多更灵活的特性，
    可以被继承、可以有方法、可以有各种各样的类变量，ReentrantLock比synchronized的扩展性体现在几点上： 
    （1）ReentrantLock可以对获取锁的等待时间进行设置，这样就避免了死锁 
    （2）ReentrantLock可以获取各种锁的信息 
    （3）ReentrantLock可以灵活地实现多路通知 
    另外，二者的锁机制其实也是不一样的:ReentrantLock底层调用的是Unsafe的park方法加锁，
    synchronized操作的应该是对象头中mark word。


### 17、Java当中有哪几种锁
    1、自旋锁: 自旋锁在JDK1.6之后就默认开启了。基于之前的观察，共享数据的锁定状态只会持续很短的时间，
        为了这一小段时间而去挂起和恢复线程有点浪费，所以这里就做了一个处理，让后面请求锁的那个线程在稍等一会，
        但是不放弃处理器的执行时间，看看持有锁的线程能否快速释放。为了让线程等待，所以需要让线程执行一个忙循环也就是自旋操作。
        在jdk6之后，引入了自适应的自旋锁，也就是等待的时间不再固定了，而是由上一次在同一个锁上的自旋时间及锁的拥有者状态来决定。
    
    2、偏向锁: 在JDK1.之后引入的一项锁优化，目的是消除数据在无竞争情况下的同步原语。进一步提升程序的运行性能。 
        偏向锁就是偏心的偏，意思是这个锁会偏向第一个获得他的线程，如果接下来的执行过程中，改锁没有被其他线程获取，
        则持有偏向锁的线程将永远不需要再进行同步。偏向锁可以提高带有同步但无竞争的程序性能，也就是说他并不一定总是对程序运行有利，
        如果程序中大多数的锁都是被多个不同的线程访问，那偏向模式就是多余的，在具体问题具体分析的前提下，可以考虑是否使用偏向锁。
    
    3、轻量级锁: 为了减少获得锁和释放锁所带来的性能消耗，引入了“偏向锁”和“轻量级锁”，所以在Java SE1.6里锁一共有四种状态，
        无锁状态，偏向锁状态，轻量级锁状态和重量级锁状态，它会随着竞争情况逐渐升级。锁可以升级但不能降级，
        意味着偏向锁升级成轻量级锁后不能降级成偏向锁。


### 18、


## 五、常用方法

### 1、两个对象值相同(x.equals(y) == true)，但却可有不同的hash code，这句话对不对？
   不对，如果两个对象x和y满足x.equals(y) == true，它们的哈希码（hash code）应当相同。
   Java对于eqauls方法和hashCode方法是这样规定的：(1)如果两个对象相同（equals方法返回true），
   那么它们的hashCode值一定要相同；(2)如果两个对象的hashCode相同，它们并不一定相同。
   当然，你未必要按照要求去做，但是如果你违背了上述原则就会发现在使用容器时，
   相同的对象可以出现在Set集合中，同时增加新元素的效率会大大下降（对于使用哈希存储的系统，
   如果哈希码频繁的冲突将会造成存取性能急剧下降）。
   
    补充：关于equals和hashCode方法，很多Java程序都知道，但很多人也就是仅仅知道而已，
    在Joshua Bloch的大作《Effective Java》（很多软件公司，《Effective Java》、
    《Java编程思想》以及《重构：改善既有代码质量》是Java程序员必看书籍，如果你还没看过，
    那就赶紧去亚马逊买一本吧）中是这样介绍equals方法的：
    首先equals方法必须满足自反性（x.equals(x)必须返回true）、
    对称性（x.equals(y)返回true时，y.equals(x)也必须返回true）、
    传递性（x.equals(y)和y.equals(z)都返回true时，x.equals(z)也必须返回true）
    和一致性（当x和y引用的对象信息没有被修改时，多次调用x.equals(y)应该得到同样的返回值），
    而且对于任何非null值的引用x，x.equals(null)必须返回false。
    实现高质量的equals方法的诀窍包括：
    1. 使用==操作符检查"参数是否为这个对象的引用"；
    2. 使用instanceof操作符检查"参数是否为正确的类型"；
    3. 对于类中的关键属性，检查参数传入对象的属性是否与之相匹配；
    4. 编写完equals方法后，问自己它是否满足对称性、传递性、一致性；
    5. 重写equals时总是要重写hashCode；
    6. 不要将equals方法参数中的Object对象替换为其他的类型，在重写时不要忘掉@Override注解。

### 2、如何实现对象克隆？
    有两种方式：
      1). 实现Cloneable接口并重写Object类中的clone()方法；
      2). 实现Serializable接口，通过对象的序列化和反序列化实现克隆，
            可以实现真正的深度克隆，代码如下：  
```
import java.io.ByteArrayInputStream;
import java.io.ByteArrayOutputStream;
import java.io.ObjectInputStream;
import java.io.ObjectOutputStream;
import java.io.Serializable;

public class MyUtil {

    private MyUtil() {
        throw new AssertionError();
    }

    @SuppressWarnings("unchecked")
    public static <T extends Serializable> T clone(T obj) throws Exception {
        ByteArrayOutputStream bout = new ByteArrayOutputStream();
        ObjectOutputStream oos = new ObjectOutputStream(bout);
        oos.writeObject(obj);

        ByteArrayInputStream bin = new ByteArrayInputStream(bout.toByteArray());
        ObjectInputStream ois = new ObjectInputStream(bin);
        return (T) ois.readObject();

        // 说明：调用ByteArrayInputStream或ByteArrayOutputStream对象的close方法没有任何意义
        // 这两个基于内存的流只要垃圾回收器清理对象就能够释放资源，这一点不同于对外部资源（如文件流）的释放
    }
}

下面是测试代码：
import java.io.Serializable;

/**
 * 人类
 * @author nnngu
 *
 */
class Person implements Serializable {
    private static final long serialVersionUID = -9102017020286042305L;

    private String name;    // 姓名
    private int age;        // 年龄
    private Car car;        // 座驾

    public Person(String name, int age, Car car) {
        this.name = name;
        this.age = age;
        this.car = car;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public Car getCar() {
        return car;
    }

    public void setCar(Car car) {
        this.car = car;
    }

    @Override
    public String toString() {
        return "Person [name=" + name + ", age=" + age + ", car=" + car + "]";
    }

}

/**
 * 小汽车类
 * @author nnngu
 *
 */
class Car implements Serializable {
    private static final long serialVersionUID = -5713945027627603702L;

    private String brand;       // 品牌
    private int maxSpeed;       // 最高时速

    public Car(String brand, int maxSpeed) {
        this.brand = brand;
        this.maxSpeed = maxSpeed;
    }

    public String getBrand() {
        return brand;
    }

    public void setBrand(String brand) {
        this.brand = brand;
    }

    public int getMaxSpeed() {
        return maxSpeed;
    }

    public void setMaxSpeed(int maxSpeed) {
        this.maxSpeed = maxSpeed;
    }

    @Override
    public String toString() {
        return "Car [brand=" + brand + ", maxSpeed=" + maxSpeed + "]";
    }

}

class CloneTest {

    public static void main(String[] args) {
        try {
            Person p1 = new Person("郭靖", 33, new Car("Benz", 300));
            Person p2 = MyUtil.clone(p1);   // 深度克隆
            p2.getCar().setBrand("BYD");
            // 修改克隆的Person对象p2关联的汽车对象的品牌属性
            // 原来的Person对象p1关联的汽车不会受到任何影响
            // 因为在克隆Person对象时其关联的汽车对象也被克隆了
            System.out.println(p1);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```  
注意：基于序列化和反序列化实现的克隆不仅仅是深度克隆，更重要的是通过泛型限定，
可以检查出要克隆的对象是否支持序列化，这项检查是编译器完成的，
不是在运行时抛出异常，这种是方案明显优于使用Object类的clone方法克隆对象。
让问题在编译的时候暴露出来总是好过把问题留到运行时。


### 3、


## 六、java面向对象

### 1、构造器（constructor）是否可被重写（override）？
    构造器不能被继承，因此不能被重写，但可以被重载。
    
    
### 2、是否可以继承String类？
   String 类是final类，不可以被继承。

    补充：继承String本身就是一个错误的行为，对String类型最好的重用方式是关联关系（Has-A）
    和依赖关系（Use-A）而不是继承关系（Is-A）。
    
    
### 3、当一个对象被当作参数传递到一个方法后，此方法可改变这个对象的属性，并可返回变化后的结果，那么这里到底是按值传递还是按引用传递？
    是按值传递。Java语言的方法调用只支持参数的按值传递。
    当一个对象实例作为一个参数被传递到方法中时，参数的值就是对该对象的引用。
    对象的属性可以在被调用过程中被改变，但在方法内部对对象引用的改变是不会影响到被调用者的。
    C++和C#中可以通过传引用或传输出参数来改变传入的参数的值。
    在C#中可以编写如下所示的代码，但是在Java中却做不到。
    
    
### 4、抽象类（abstract class）和接口（interface）有什么异同？
    抽象类和接口都不能够实例化，但可以定义抽象类和接口类型的引用。
    一个类如果继承了某个抽象类或者实现了某个接口都需要对其中的抽象方法全部进行实现，
    否则该类仍然需要被声明为抽象类。接口比抽象类更加抽象，因为抽象类中可以定义构造器，
    可以有抽象方法和具体方法，而接口中不能定义构造器而且其中的方法全部都是抽象方法。
    抽象类中的成员可以是private、默认、protected、public的，
    而接口中的成员全都是public的。抽象类中可以定义成员变量，
    而接口中定义的成员变量实际上都是常量。有抽象方法的类必须被声明为抽象类，
    而抽象类未必要有抽象方法。
   

### 5、静态嵌套类(Static Nested Class)和内部类（Inner Class）的不同？
    Static Nested Class是被声明为静态（static）的内部类，
    它可以不依赖于外部类实例被实例化。
    而通常的内部类需要在外部类实例化后才能实例化，其语法看起来挺诡异的，如下所示。
```
/**
 * 扑克类（一副扑克）
 *
 */
public class Poker {
    private static String[] suites = {"黑桃", "红桃", "草花", "方块"};
    private static int[] faces = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13};

    private Card[] cards;

    /**
     * 构造器
     * 
     */
    public Poker() {
        cards = new Card[52];
        for(int i = 0; i < suites.length; i++) {
            for(int j = 0; j < faces.length; j++) {
                cards[i * 13 + j] = new Card(suites[i], faces[j]);
            }
        }
    }

    /**
     * 洗牌 （随机乱序）
     * 
     */
    public void shuffle() {
        for(int i = 0, len = cards.length; i < len; i++) {
            int index = (int) (Math.random() * len);
            Card temp = cards[index];
            cards[index] = cards[i];
            cards[i] = temp;
        }
    }

    /**
     * 发牌
     * @param index 发牌的位置
     * 
     */
    public Card deal(int index) {
        return cards[index];
    }

    /**
     * 卡片类（一张扑克）
     * [内部类]
     *
     */
    public class Card {
        private String suite;   // 花色
        private int face;       // 点数

        public Card(String suite, int face) {
            this.suite = suite;
            this.face = face;
        }

        @Override
        public String toString() {
            String faceStr = "";
            switch(face) {
            case 1: faceStr = "A"; break;
            case 11: faceStr = "J"; break;
            case 12: faceStr = "Q"; break;
            case 13: faceStr = "K"; break;
            default: faceStr = String.valueOf(face);
            }
            return suite + faceStr;
        }
    }
}
``` 
测试代码：
```
class PokerTest {

    public static void main(String[] args) {
        Poker poker = new Poker();
        poker.shuffle();                // 洗牌
        Poker.Card c1 = poker.deal(0);  // 发第一张牌
        // 对于非静态内部类Card
        // 只有通过其外部类Poker对象才能创建Card对象
        Poker.Card c2 = poker.new Card("红心", 1);    // 自己创建一张牌

        System.out.println(c1);     // 洗牌后的第一张
        System.out.println(c2);     // 打印: 红心A
    }
}
```
---面试题 - 下面的代码哪些地方会产生编译错误？
```
class Outer {

    class Inner {}

    public static void foo() { new Inner(); }

    public void bar() { new Inner(); }

    public static void main(String[] args) {
        new Inner();
    }
}
```
注意：Java中非静态内部类对象的创建要依赖其外部类对象，
    上面的面试题中foo和main方法都是静态方法，静态方法中没有this，
    也就是说没有所谓的外部类对象，因此无法创建内部类对象，
    如果要在静态方法中创建内部类对象，可以这样做：
```
    new Outer().new Inner();
```
    

### 6、抽象的（abstract）方法是否可同时是静态的（static）,是否可同时是本地方法（native），是否可同时被synchronized修饰？
    都不能。
    抽象方法需要子类重写，而静态的方法是无法被重写的，因此二者是矛盾的。
    本地方法是由本地代码（如C代码）实现的方法，而抽象方法是没有实现的，也是矛盾的。
    synchronized和方法的实现细节有关，抽象方法不涉及实现细节，因此也是相互矛盾的。


### 7、阐述静态变量和实例变量的区别。
    静态变量是被static修饰符修饰的变量，也称为类变量，它属于类，
    不属于类的任何一个对象，一个类不管创建多少个对象，静态变量在内存中有且仅有一个拷贝；
    实例变量必须依存于某一实例，需要先创建对象然后通过对象才能访问到它。
    静态变量可以实现让多个对象共享内存。
    
    
### 8、是否可以从一个静态（static）方法内部发出对非静态（non-static）方法的调用？
    不可以，静态方法只能访问静态成员，因为非静态方法的调用要先创建对象，
    在调用静态方法时可能对象并没有被初始化。
    
    
### 9、接口是否可继承（extends）接口？抽象类是否可实现（implements）接口？抽象类是否可继承具体类（concrete class）？
    接口可以继承接口，而且支持多重继承。
    抽象类可以实现(implements)接口，抽象类可继承具体类也可以继承抽象类。
    

### 10、一个".java"源文件中是否可以包含多个类（不是内部类）？有什么限制？
    可以，但一个源文件中最多只能有一个公开类（public class）
    而且文件名必须和公开类的类名完全保持一致。
    
    
### 11、Anonymous Inner Class(匿名内部类)是否可以继承其它类？是否可以实现接口？
    可以继承其他类或实现其他接口，在Swing编程和Android开发中常用此方式来实现事件监听和回调。
    
    
### 12、运行时异常与受检异常有何异同？
           异常表示程序运行过程中可能出现的非正常状态，
           运行时异常表示虚拟机的通常操作中可能遇到的异常，是一种常见运行错误，
           只要程序设计得没有问题通常就不会发生。受检异常跟程序运行的上下文环境有关，
           即使程序设计无误，仍然可能因使用的问题而引发。
           Java编译器要求方法必须声明抛出可能发生的受检异常，
           但是并不要求必须声明抛出未被捕获的运行时异常。
           异常和继承一样，是面向对象程序设计中经常被滥用的东西，
           在Effective Java中对异常的使用给出了以下指导原则：
```
       不要将异常处理用于正常的控制流（设计良好的API不应该强迫它的调用者为了正常的控制流而使用异常）
       对可以恢复的情况使用受检异常，对编程错误使用运行时异常
       避免不必要的使用受检异常（可以通过一些状态检测手段来避免异常的发生）
       优先使用标准的异常
       每个方法抛出的异常都要有文档
       保持异常的原子性
       不要在catch中忽略掉捕获到的异常
```


### 13、重载（Overload）和重写（Override）的区别。重载的方法能否根据返回类型进行区分？
    方法的重载和重写都是实现多态的方式，区别在于前者实现的是编译时的多态性，
    而后者实现的是运行时的多态性。重载发生在一个类中，
    同名的方法如果有不同的参数列表（参数类型不同、参数个数不同或者二者都不同）则视为重载；
    重写发生在子类与父类之间，重写要求子类被重写方法与父类被重写方法有相同的返回类型，
    比父类被重写方法更好访问，不能比父类被重写方法声明更多的异常（里氏代换原则）。
    重载对返回类型没有特殊的要求。


### 14、

## 七、JVM

### 1、描述一下JVM加载class文件的原理机制？
    JVM中类的装载是由类加载器（ClassLoader）和它的子类来实现的，
    Java中的类加载器是一个重要的Java运行时系统组件，它负责在运行时查找和装入类文件中的类。
    由于Java的跨平台性，经过编译的Java源程序并不是一个可执行程序，
    而是一个或多个类文件。当Java程序需要使用某个类时，
    JVM会确保这个类已经被加载、连接（验证、准备和解析）和初始化。
    类的加载是指把类的.class文件中的数据读入到内存中，
    通常是创建一个字节数组读入.class文件，然后产生与所加载类对应的Class对象。
    加载完成后，Class对象还不完整，所以此时的类还不可用。当类被加载后就进入连接阶段，
    这一阶段包括验证、准备（为静态变量分配内存并设置默认的初始值）
    和解析（将符号引用替换为直接引用）三个步骤。最后JVM对类进行初始化，
    包括：
    1)如果类存在直接的父类并且这个类还没有被初始化，那么就先初始化父类；
    2)如果类中存在初始化语句，就依次执行这些初始化语句。
    类的加载是由类加载器完成的，
    类加载器包括：根加载器（BootStrap）、扩展加载器（Extension）、
              系统加载器（System）和用户自定义类加载器（java.lang.ClassLoader的子类）。
    从Java 2（JDK 1.2）开始，类加载过程采取了父亲委托机制（PDM）。
    PDM更好的保证了Java平台的安全性，在该机制中，JVM自带的Bootstrap是根加载器，
    其他的加载器都有且仅有一个父类加载器。类的加载首先请求父类加载器加载，
    父类加载器无能为力时才由其子类加载器自行加载。JVM不会向Java程序提供对Bootstrap的引用。
    下面是关于几个类加载器的说明：
    
    Bootstrap：一般用本地代码实现，负责加载JVM基础核心类库（rt.jar）；
    Extension：从java.ext.dirs系统属性所指定的目录中加载类库，它的父加载器是Bootstrap；
    System：又叫应用类加载器，其父类是Extension。它是应用最广泛的类加载器。
        它从环境变量classpath或者系统属性java.class.path所指定的目录中加载类，
        是用户自定义加载器的默认父加载器。
        
        
### 2、解释内存中的栈(stack)、堆(heap)和方法区(method area)的用法。
    通常我们定义一个基本数据类型的变量，一个对象的引用，
    还有就是函数调用的现场保存都使用JVM中的栈空间；
    而通过new关键字和构造器创建的对象则放在堆空间，堆是垃圾收集器管理的主要区域，
    由于现在的垃圾收集器都采用分代收集算法，所以堆空间还可以细分为新生代和老生代，
    再具体一点可以分为Eden、Survivor（又可分为From Survivor和To Survivor）、Tenured；
    方法区和堆都是各个线程共享的内存区域，
    用于存储已经被JVM加载的类信息、常量、静态变量、JIT编译器编译后的代码等数据；
    程序中的字面量（literal）如直接书写的100、"hello"和常量都是放在常量池中，常量池是方法区的一部分，。
    栈空间操作起来最快但是栈很小，通常大量的对象都是放在堆空间，
    栈和堆的大小都可以通过JVM的启动参数来进行调整，栈空间用光了会引发StackOverflowError，
    而堆和常量池空间不足则会引发OutOfMemoryError。
```
    补充1：较新版本的Java（从Java 6的某个更新开始）中，
    由于JIT编译器的发展和"逃逸分析"技术的逐渐成熟，
    栈上分配、标量替换等优化技术使得对象一定分配在堆上这件事情已经变得不那么绝对了。
    补充2：运行时常量池相当于Class文件常量池具有动态性，
    Java语言并不要求常量一定只有编译期间才能产生，运行期间也可以将新的常量放入池中，
    String类的intern()方法就是这样的。
``` 
    


### 3、解释jvm内存结构：

    
### 4、Java 中会存在内存泄漏吗，请简单描述。
    理论上Java因为有垃圾回收机制（GC）不会存在内存泄露问题
    （这也是Java被广泛使用于服务器端编程的一个重要原因）；
    然而在实际开发中，可能会存在无用但可达的对象，这些对象不能被GC回收，
    因此也会导致内存泄露的发生。例如Hibernate的Session（一级缓存）中的对象属于持久态，
    垃圾回收器是不会回收这些对象的，然而这些对象中可能存在无用的垃圾对象，
    如果不及时关闭（close）或清空（flush）一级缓存就可能导致内存泄露。
    下面例子中的代码也会导致内存泄露。
```
import java.util.Arrays;
import java.util.EmptyStackException;

public class MyStack<T> {
    private T[] elements;
    private int size = 0;

    private static final int INIT_CAPACITY = 16;

    public MyStack() {
        elements = (T[]) new Object[INIT_CAPACITY];
    }

    public void push(T elem) {
        ensureCapacity();
        elements[size++] = elem;
    }

    public T pop() {
        if(size == 0) 
            throw new EmptyStackException();
        return elements[--size];
    }

    private void ensureCapacity() {
        if(elements.length == size) {
            elements = Arrays.copyOf(elements, 2 * size + 1);
        }
    }
}
```
    上面的代码实现了一个栈（先进后出（FILO））结构，乍看之下似乎没有什么明显的问题，
    它甚至可以通过你编写的各种单元测试。然而其中的pop方法却存在内存泄露的问题，
    当我们用pop方法弹出栈中的对象时，该对象不会被当作垃圾回收，
    即使使用栈的程序不再引用这些对象，因为栈内部维护着对这些对象的过期引用
    （obsolete reference）。在支持垃圾回收的语言中，内存泄露是很隐蔽的，
    这种内存泄露其实就是无意识的对象保持。如果一个对象引用被无意识的保留起来了，
    那么垃圾回收器不会处理这个对象，也不会处理该对象引用的其他对象，
    即使这样的对象只有少数几个，也可能会导致很多的对象被排除在垃圾回收之外，
    从而对性能造成重大影响，极端情况下会引发Disk Paging（物理内存与硬盘的虚拟内存交换数据），
    甚至造成OutOfMemoryError。
    

### 5、GC是什么？为什么要有GC？
    GC是垃圾收集的意思，内存处理是编程人员容易出现问题的地方，
    忘记或者错误的内存回收会导致程序或系统的不稳定甚至崩溃，
    Java提供的GC功能可以自动监测对象是否超过作用域从而达到自动回收内存的目的，
    Java语言没有提供释放已分配内存的显式操作方法。Java程序员不用担心内存管理，
    因为垃圾收集器会自动进行管理。要请求垃圾收集，可以调用下面的方法之一：
    System.gc() 或Runtime.getRuntime().gc() ，但JVM可以屏蔽掉显式的垃圾回收调用。
    垃圾回收可以有效的防止内存泄露，有效的使用可以使用的内存。
    垃圾回收器通常是作为一个单独的低优先级的线程运行，
    不可预知的情况下对内存堆中已经死亡的或者长时间没有使用的对象进行清除和回收，
    程序员不能实时的调用垃圾回收器对某个对象或所有对象进行垃圾回收。
    在Java诞生初期，垃圾回收是Java最大的亮点之一，
    因为服务器端的编程需要有效的防止内存泄露问题，然而时过境迁，
    如今Java的垃圾回收机制已经成为被诟病的东西。
    移动智能终端用户通常觉得iOS的系统比Android系统有更好的用户体验，
    其中一个深层次的原因就在于Android系统中垃圾回收的不可预知性。
    
补充：垃圾回收机制有很多种，
    包括：分代复制垃圾回收、标记垃圾回收、增量垃圾回收等方式。
    标准的Java进程既有栈又有堆。栈保存了原始型局部变量，堆保存了要创建的对象。
    Java平台对堆内存回收和再利用的基本算法被称为标记和清除，但是Java对其进行了改进，
    采用“分代式垃圾收集”。这种方法会根据Java对象的生命周期将堆内存划分为不同的区域，
    在垃圾收集过程中，可能会将对象移动到不同区域：
    
        伊甸园（Eden）：这是对象最初诞生的区域，并且对大多数对象来说，这里是它们唯一存在过的区域。
        幸存者乐园（Survivor）：从伊甸园幸存下来的对象会被挪到这里。
        终身颐养园（Tenured）：这是足够老的幸存对象的归宿。年轻代收集（Minor-GC）过程是不会触及这个地方的。当年轻代收集不能把对象放进终身颐养园时，就会触发一次完全收集（Major-GC），这里可能还会牵扯到压缩，以便为大对象腾出足够的空间。

与垃圾回收相关的JVM参数：

    -Xms / -Xmx — 堆的初始大小 / 堆的最大大小
    -Xmn — 堆中年轻代的大小
    -XX:-DisableExplicitGC — 让System.gc()不产生任何作用
    -XX:+PrintGCDetails — 打印GC的细节
    -XX:+PrintGCDateStamps — 打印GC操作的时间戳
    -XX:NewSize / XX:MaxNewSize — 设置新生代大小/新生代最大大小
    -XX:NewRatio — 可以设置老生代和新生代的比例
    -XX:PrintTenuringDistribution — 设置每次新生代GC后输出幸存者乐园中对象年龄的分布
    -XX:InitialTenuringThreshold / -XX:MaxTenuringThreshold：
                                            设置老年代阀值的初始值和最大值
    -XX:TargetSurvivorRatio：设置幸存区的目标使用率


### 6、
   
    
## 六、java I/O、NIO、

### 1、Java中有几种类型的流？
    字节流和字符流。字节流继承于InputStream、OutputStream，
    字符流继承于Reader、Writer。在 java.io 包中还有许多其他的流，
    主要是为了提高性能和使用方便。
    关于Java的I/O需要注意的有两点：
    一是两种对称性（输入和输出的对称性，字节和字符的对称性）；
    二是两种设计模式（适配器模式和装潢模式）。
    另外Java中的流不同于C#的是它只有一个维度一个方向。
  
    
    
    
    
    
    