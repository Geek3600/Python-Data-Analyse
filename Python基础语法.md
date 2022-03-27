# Python

***

## 基本语法

1. 在python中的变量是在特殊命名空间中的对象的名字

   类型信息保存在对象自身中。(万物皆对象)

2. python的对象通常有属性（储存在对象内部）和方法

   可以用**obj.attribute_name**访问属性和方法，也可以使用**getattr**函数

   * getattr(a, 'split')

3. 鸭子类型：用一个类创建了一个对象，里面有属性和方法，但我们要用他时，可能并不关心对象是什么类型，而关心有什么方法，这通常叫做 “ 鸭子类型 ”。

***

## 数据类型和序列

### 元组

1. 基本性质：元组是一种固定长度，不可改变的python序列对象，最简单的创建方式为用逗号分隔一列值

​       In [1]: tup = 4, 5, 6

​       In [2]: tup
​       Out[2]: (4, 5, 6)

2. 创建注意事项：当用复杂的表达式定义元组，最好将值放到圆括号内

   In [3]: nested_tup = (4, 5, 6), (7, 8)

   In [4]: nested_tup
   Out[4]: ((4, 5, 6), (7, 8))

   

3. 类型转换：用**tuple()**可以将任意序列或迭代器转换为元组，即强制类型转换.

    

4. 元组元素的访问：用方括号内加元素的序列号(即下标)

   In [8]: tup[0]

   

5. 元素性质： 元组中储存的对象可能是可变对象，但是元组一旦创建，元组中的对象就不能修改了。如果元组中的某个对象是可变的，比如列表，那么就可以在原位进行修改

   In [11]: tup[1].append(3)

   In [12]: tup
   Out[12]: ('foo', [1, 2, 3], True)

   

6. 元组串联： 用加法运算符，**当某个元组只有一个元素时，要加一个尾随逗号**（这么做的原因是：当元组只有一个元素时，解释器可能会将这个单元素的元组当作一个整型变量，如果加了一个尾随逗号，则相当于给解释器提示这是一个元组）

   In [13]:   ( 4, None, ' foo ')  +  (6, 0)  + ( 'bar' , )
   Out[13]:  ( 4, None, ' foo ' , 6, 0,  ' bar ' )

   

7. 拆分元组：

   * 如果你想将元组赋值给类似元组的变量，Python会试图拆分等号右边的值

     ![image-20220301210904377](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220301210904377.png)

     

   * 即使含有元组的元组也会被拆分：

     ![image-20220301211501834](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220301211501834.png)

     

   * 使用元组的拆分赋值的功能，我们可以比其他语言更容易地交换两个变量

   ​       ![image-20220301212021495](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220301212021495.png)

   

   * 变量拆分常用来迭代元组或列表序列![image-20220301222040963](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220301222040963.png) 

   * *rest功能：允许从开头摘取部分元素，剩下的全部元素**变为列表类型**保存在 rest变量中![image-20220301222720396](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220301222720396.png)

     

     rest的部分是想要舍弃的部分，rest的名字不重要，通常人们会将不需要的变量使用下划线![image-20220301222940016](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220301222940016.png)

8. tuple方法：由于元组一旦创建，大小和内容就无法被改变，所以他的实例方法都很轻量，其中最有用的就是**count函数**

   * count函数：可以统计某个值出现的频率![image-20220301225734475](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220301225734475.png)

***



### 列表

***

1. 与元组相比，列表长度可变，内容可以被修改，用方括号[ ]定义，或用 list 函数创建列表（ 其实用 list() 函数相当于强制类型转换）![image-20220302161540994](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220302161540994.png)

   列表和元组的语义接近，在许多函数中可以交叉使用

2. 列表的添加和删除元素

   * append()：在**列表末尾**添加一个元素![image-20220302162050704](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220302162050704.png)

   * insert( index, obj): 在**特定位置**插入元素

     * index : 插入位置的索引

     * obj : 插入内容![image-20220302162436706](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220302162436706.png)

     ​       插入的序号必须在0和 列表长度之间

     * 与append相比，insert耗费的计算量很大，因为每次插入都要将插入位置的后续元素进行平移

   * pop(index) : insert() 的逆过程，**移除**并**返回**指定位置的元素![image-20220302163354643](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220302163354643.png)

   * remove() : 直接移除列表的第一个元素![image-20220302164310951](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220302164310951.png)

3. in可以检查列表中是否包含某个值![image-20220302164627215](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220302164627215.png)

   否定in 还可以在in前面加一个 not![image-20220302164640329](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220302164640329.png)

4. 列表串联与组合

   * 加号串联多个列表
   * extend追加列表元素![image-20220302164946793](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220302164946793.png)
     * 追加元素 extend() 要比 加号 串联的方法更快![image-20220302165247492](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220302165247492.png)
     * extend与append的区别![image-20220302165717199](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220302165717199.png)

5. 排序：sort()将列表原地排序，有一些关键字参数可实现不同的排序方式![image-20220302170118392](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220302170118392.png)

6. 二分查找和维护已排序的列表

   * bisect模块支持**二分查找** 和向**已排序的列表**插入值
     * bisect.bisect():找到插入值的位置，并返回索引,仍保持排序的位置
     * bisect.insort(list, obj): 按列表的内部顺序插入obj内容

7. **切片**:

   * 基本形式：list[start : stop]  
   * 切片内容的 包括起始元素，不包括结束元素
   * start 和 stop 均可以省略，省略后就默认从列表的开头或结尾
   * start和stop可以是负数，如果是负数，则从后面开始切片
   * ![image-20220302184600143](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220302184600143.png)
   * 间隔形式：list[start：stop：step]
   * step：为步长，即间隔取值
   * 当step为-1时会把列表或元组元素顺序颠倒，但是这样4做并不会改变原列表或数组![image-20220302185058802](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220302185058802.png)



***

### 字典

  字典可能是Python最为重要的数据结构。它更为常见的名字是哈希映射或关联数组。它是键值对的大小可变集合，键和值都是Python对象。创建字典的方法之一是使用尖括号，用冒号分隔键和值![image-20220302200123418](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220302200123418.png)

* 基本形式 dict1 = { key：value，.....}
* 索引方式：dict1[key] = value
* 可用 in 检查字典中是否含有某个键，与检查列表和元组一样

1. del函数：删除任意指定元素，注意这是个函数，不是字典的方法，![image-20220302211122313](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220302211122313.png)

2. pop(key) 方法：移除字典中的指定的键值，并将值返回![image-20220302211349039](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220302211349039.png)

   

3. keys() 方法 ：迭代读取字典中所有的键，并一起返回

   values()方法：迭代读取字典中所有的值，并一起返回![image-20220302211725811](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220302211725811.png)

4. update(dict)方法：将一个字典与另一个字典融合，改变原来的字典，新值会覆盖旧值![image-20220302212055426](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220302212055426.png)

   

5. get( key, default_value)方法: 返回键为key的值，如果字典内没有这个key，默认返回None![image-20220302213625990](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220302213625990.png)

6. setdefault方法

   * setfault(key, value)
   * 返回指定键的值，如果指定的键不存在，则将value值作为新创建的key的值![image-20220302215250753](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220302215250753.png)

7. **有效的键类型**：

   * 字典的值可以是任意Python对象

   * 键通常是**不可变**的数据类型：整数、浮点、字符串或元组，称为“**可哈希性**”，可用“**hash函数**”检测一个对象**是否是可哈希的**（可以作为字典的键）![image-20220302230532243](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220302230532243.png)![image-20220302230603685](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220302230603685.png)

     如果hash检测返回的是数值，则可作为字典的键，如果报错则不可被哈希





***

### 集合

 集合(set)是无序的不可重复的元素的集合，相当于**只有键没有值**的字典。

1. 集合的创建：

   * set函数：![image-20220302231816376](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220302231816376.png)
   * 直接创建：用尖括号![image-20220302232035533](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220302232035533.png)

2. 集合的运算：合并(并集)， 交集，差分和对称差等数学集合运算

   

   * 合并(并集)：union方法 或 | 运算符![image-20220303094627255](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220303094627255.png)
   * 交集：用 intersection方法或 & 运算符![image-20220303094823082](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220303094823082.png)
   * 其他常用方法![image-20220303095725617](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220303095725617.png)

### 列表、集合和字典推导式

#### 列表推导式：

​         [ 表达式  for  迭代变量 in 可迭代对象  [ if 条件表达式 ] 

* 列表推导式的语法格式其实是对for循环语句进行了变形，实际上的执行顺序是这样的，

  ![image-20220303100757426](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220303100757426.png)

* 不同在于：列表推导式最终会将循环过程中计算得到的一系列值组成一个列表![image-20220303101338825](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220303101338825.png)

* 注意！别漏掉语句外围的方括号

#### 字典推导式

  dict_comp = { key_expr : value_expr  for value in collection if condition }

* 注意要尖括号，键和值的表达式

#### 集合推导式

   set_comp = { expr for value in collection  if condition}

* 尖括号

#### map函数

​           map(funciton, iterable,...) 函数可以简化各序列推导式

1. map 函数会根据我们提供的函数对指定序列的每一个元素进行函数操作，并得到一个新的返回值（**注意对返回值进行类型转换**）![image-20220303130153503](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220303130153503.png)

#### 嵌套列表推导式![image-20220303131232482](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220303131232482.png)

​     由图可见，嵌套列表的表达式的阅读顺序式**从左到右**，对应的列表读取顺序式**由外到内**

* 用法案例：元组列表扁平化![image-20220303135856893](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220303135856893.png)





***

### 序列函数：

​    Python有一些序列函数

1. **enumerate函数**：追踪一个序列内部所有元素的索引和元素值，并作为一个二元元组返回，一般搭配for使用![image-20220302185920203](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220302185920203.png)

   * enumerate 的一种用法，将对应的索引和元素值，转换为字典的key和值（用enumerate将列表转换为字典）![image-20220302190450862](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220302190450862.png)

2. **sorted函数**：

   * sorted(iterable, cmp=None, key=None, reverse=False)

   * iterable: 可迭代的对象

   * cmp：lambda x:x[?] 是固定写法，x其实可以为任意值

   * key：lambda x:x[?] 是固定写法，x其实可以为任意值。key是作为排序的标准。

     * **lambda函数**:相当于给我们提供了一个不用名字就可以使用的函数

     * ![image-20220302192639502](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220302192639502.png)

     * ![image-20220302192707801](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220302192707801.png)

       

   * reverse：True时为降序，False为升序

   **sort和sorted的区别**

   * sort() 是列表的内置方法，只修改原来的列表
   * sorted() 可以作用于所有可迭代对象，排序之后会生成一个新的对象并返回，*不修改原来的迭代对象*

3. **zip函数**：可以将多个列表、元组或其他序列**成对组合**成一个元组列表，最终要记得**类型转换**才能展示出来![image-20220302193214148](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220302193214148.png)

   

   * zip函数可以处理任意多的序列，但最终的元素的个数取决于最短序列(木桶效应)![image-20220302193631159](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220302193631159.png)

     

   * zip函数常见方法之一，搭配enumerate函数迭代多个序列![image-20220302194215862](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220302194215862.png)

     

   * zip解压缩功能，即zip可以逆用之前的功能，解压序列![image-20220302195837713](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220302195837713.png)

4. **reversed函数**

   * reversed是一个生成器

***

## 函数

### 函数参数

1. 函数可能会有一些 位置参数(positional) 和 关键字参数(keyword), 关键字参数通过用于指定默认值或可选参数

   * 参数限制：关键字参数必须位于位置参数之后。

   * 调用方式：

     ![image-20220303141628188](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220303141628188.png)

### 命名空间、作用域和局部函数

   函数可以访问两种不同作用域中的变量：全局变量(global)、局部变量(local)。Pyhon中有一种描述变量作用域的名称，即**命名空间（namespace）**

* 任何在函数中赋值的对象默认都是被分配到局部命名空间
* 局部命名空间是在函数被调用时创建的，函数参数会立即填入该命名空间，但在函数执行完之后，局部命名空间就会被销毁

![image-20220303142924753](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220303142924753.png)

​         调用func()之后，首先会创建出空列表a，然后添加5个元素，最后a         会在 该函数退出的时候被销毁。假如我们像下面这样定义a：

![image-20220303142958206](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220303142958206.png)

虽然可以在函数中对全局变量进行赋值操作，但是那些变量必须用global关键字声明成全局 (global) 的才行：

![image-20220303143042032](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220303143042032.png)

### 返回值

  Pyhon的函数可以返回多个值

* 函数其实是返回一个元组，如果只用一个变量接收，那么就是元组，如果，用元组拆分的方式借助多个变量接收
* 我们还可以自己定义返回值形式![image-20220303144558446](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220303144558446.png)

### 函数也是对象

​      由于Python函数也是对象，所以我们可以在一组给定字符串上执行的所有函数运算做成一个列表(很神奇的操作)![image-20220303151237057](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220303151237057.png)

* **lambda函数**：Python的匿名函数，由单挑语句组成，该语句的结果就是返回值。lambda函数的特点：就是可以执行类似函数的功能，但是不需要对他取名(匿名)，lambda函数在作为函数参数时很常见
  * 基本形式：lambda x :  expr 是固定写法，x其实可以为任意值

### 柯里化

​              即部分参数应用

![image-20220303152835904](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220303152835904.png)

* 这里由内置的functools模块可以用partial函数简化

  ![image-20220303152853589](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220303152853589.png)

## 生成器

​       在Python中一边循环一边计算的机制，称为生成器(generator)

* 生成器本质：一种生成数据的算法，可以在需要数据时调用生成器生成数据。

* 意义：有了生成器，我们不必创建完整的list去存储数据，而是知道数据的规律，通过生成器算法在我们需要的时候临时生成数据，可以极大地节省空间

* 生成器创建：

  * 把列表推导式的[ ]改为（），就创建了一个generator
  * 函数中包含yield关键字，那么这个函数就不再是一个普通函数，而是一个generator。调用该函数就是调用了generator对象

* 生成器工作原理：(截图内容来源于https://www.cnblogs.com/liangmingshen/p/9706181.html)

  ![image-20220303155951314](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220303155951314.png)

* itertools模块

  标准库itertools模块中有一组用于许多常见数据算法的生成器。例如，groupby可以接受任何序列和一个函数，他根据函数的返回值对序列中的连续元素进行分组

  * groupby()的作用就是把可迭代对象中的**满足指定条件的元素**挑出来合并在一起组成一个个小列表![image-20220303163135934](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220303163135934.png)

## 错误与异常处理

  优雅地处理Python的错误和异常是构建健壮程序的重要部分。在数据分析中，许多函数只用于部分输入。例如，Python的float函数可以将字符串转换成浮点数，但输入有误时，有`ValueError`错误：![image-20220303163525327](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220303163525327.png)

假如想优雅地处理float的错误，让它返回输入值。我们可以写一个函数，在try/except中调用float：![image-20220303163545563](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220303163545563.png)

* 当float(x)抛出异常时，才会执行except部分
* 你可能注意到float抛出的异常不仅是ValueError：![image-20220303163711581](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220303163711581.png)
* 你可能只想处理ValueError，TypeError错误（输入不是字符串或数值）可能是合理的bug。可以写一个异常类型：![image-20220303163732042](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220303163732042.png)
* 可以用**元组包含**多个异常：![image-20220303164042215](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220303164042215.png)
* 某些情况下，我们可能不想抑制异常，我们想无论try部分的代码是否成功，都能执行一段代码，可以使用**finally**：![image-20220303164656540](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220303164656540.png)

***

## 文件和操作系统

* 为了打开一个文件以便读写，可以使用内置的open函数以及一个相对或绝对的文件路径：![image-20220303165504989](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220303165504989.png)
* 默认情况下，文件是以只读模式（'r'）打开的。然后，我们就可以像处理列表那样来处理这个文件句柄f了，比如对行进行迭代
* 文件的读\写模式：![image-20220303165711916](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220303165711916.png)
* 对于可读文件，一些常用的方法是read、seek和tell。
  * read会从文件返回字符。read模式会将文件句柄的位置提前，提前的数量是读取的字节数。
  * seek将文件位置更改为文件中的指定字节。
  * 向文件写入，可以使用文件的write或writelines方法。
* 常用的文件方法：![image-20220303165947935](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220303165947935.png)

***

