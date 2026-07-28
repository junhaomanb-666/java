![78453306141](C:\Users\mjhqu\AppData\Local\Temp\1784533061418.png)

![img](https://uploadfiles.nowcoder.com/images/20190618/117596164_1560821319150_ACED241801E307EE7A39612F85A94EBF)



这个问题我试着回答一下，同时也是相互学习。String str1= "hello",      String
str2="he"+"llo";之所以str1==str2返回true是因为两者都是在字符串常量池中（由于初始化就会在此区域分布内存）而常量池中的有个与栈区类似的特性，就是当str2指向的常量在常量区已存在时，他不会创建新的内存空间来存此常量，而是指向已有常量的内存（应该是以此节约空间），此时str1与str2这两个引用变量的值都是存"hello"的内存空间地址，但是String
str3= "he"+a;String a="llo";时str1==str3返回的为false，是因为：str1指向的hello在编译期一如既往的还是分配在常量区内，a指向的llo也在常量区，虽然str3也是初始化但是编译器无法判断a这货到底是什么个情况，进而不会将str3的等号右侧声明在常量区内，而是在通过构造时在堆区中的非常量池外的内存中声明，至此str3与str1不止是分配内存的时期不同（一个在编译期，一个在运行期）而且在内存空间的区域也不同，上面最高票答案只区分了时间没区分空间。

![78454203119](C:\Users\mjhqu\AppData\Local\Temp\1784542031190.png)

 通俗的讲，就是基本数据类型和包装类之间的转换。如： int  类型和  Integer  类的转换

  基本数据类型转化成包装类是装箱  (如： int  -->  Integer)。
 包装类转化成基本数据类型就是拆箱 
  (如：Integer  -->  int)。
 包装类就是引用类型，基本数据类型就是值类型。

![78454211760](C:\Users\mjhqu\AppData\Local\Temp\1784542117608.png)

*其他三个都是web服务器*

*LVS是*Linux Virtual Server的简写，意即Linux虚拟服务器，是一个虚拟的服务器集群系统 

![78454217179](C:\Users\mjhqu\AppData\Local\Temp\1784542171792.png)

在源码中  toLowerCase  是重新  new String()

  ![img](https://uploadfiles.nowcoder.com/images/20170314/184838_1489466288980_4A47A0DB6E60853DEDFCFDF08A5CA249)

  所以为  ==  是比较对象是否是同一个对象，所以为  false