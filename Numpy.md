# Numpy

***

## Numpy的优点： 

* Numpy是在一个连续的内存块中存储数据，独立于其他的Python内置对象（元组，列表等）。Numpy的C语言编写的算法库可以操作内存，而不必进行类型检查或其他前期的工作

* 比起Python的内置序列，Numpy数组使用的内存更少

* Numpy可以在整个数组上执行复杂的操作，而不需要Python的for循环

  ![image-20220303184142835](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220303184142835.png)

  ​     由此可见，Numpy数组运算速度远快于Python内置序列的速度

***

## ndarray

* ndarray： 一种多维数组对象，注意：ndarray不是list！！ndarry是一种独立于Python内置对象的专属于Numpy模块的新对象
* Numpy最重要的一个特点就是其**N维数组对象**(即 ndarray)， 该对象是一个快速而灵活的大数据集容器。你可以利用这种数组对整块数据进行一些数学运算，其语法跟标量元素之间的运算一样
* ndarray 是一个通用的**同构数据多维容器**。其中所有数据都是**相同类型**的。
* 每个数组都有一个 **shape **(一个**表示数组各维度大小**的**元组**)和一个 **dtype**(一个用于**说明数组数据类型**的对象)，和**ndim**(表示**当前数组的维度数**)
* 数组，Numpy数组，ndarray基本上都指的是同一样东西，即**ndarray对象**



***

## 创建ndarray

1. 创建方法：

   * np.array()函数![image-20220303212249500](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220303212249500.png)

     当输入序列为**嵌套序列**(如由等长列表组成的列表)时，将会被转换成为**多维数组**

   * np.array会尝试为新建的数组推断出一个较为合适的数据类型。数据类型保存在一个特殊的的dtype对象中。![image-20220303213059699](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220303213059699.png)

   其他的数组创建函数：

   * **np.zeros( )**和**np.ones( )**分别可以创建**指定长度或形状**的全0或全1的数组。

   * **np.empty**可以创建一个**没有任何固定数值**的数组

     ps： empty很多情况下返回的都是一些垃圾值数组，并不是固定值

   * 以上方法创建多维数组，只需要传入一个**表示形状的元组**即可，因为这类数组内部的元素都已经定下，所以我们只需要指定数组的大小即可

   * **np.arange(start, stop, step)** 是 Python内置函数 range 的 Numpy数组版，生成的是永远**一维数组**![image-20220303214756031](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220303214756031.png)

   * 其他数组创建函数。由于Numpy关注的是**数值计算**，因此，数组的数据类型**默认为float64**![image-20220303215214429](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220303215214429.png)

   

***

## ndarray数据类型

1. dtype(数据类型)是一个特殊的对象，它含有ndarray将内存解释为特定数据类型所需的信息。

2. 数值型dtype的**命名规则**：

   一个**类型名**（如float或int)，后面跟一个用于表示各元素**位长**的数字

   * 如标准的双精度浮点数据(Python中的float对象)需要占用8字节(即64位)，因此为dtype=np.float64![image-20220303220810568](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220303220810568.png)

3. **数据类型转换**：**astype方法**

   * 基本形式：array_obj.astype(np.float64)![image-20220303221456058](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220303221456058.png)

   

   * 整数转换为浮点数时，小数部分会被直接截取删除![image-20220303221513511](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220303221513511.png)

   * 如果字符串数组表示的全是数字，也可以用astype将其表示为数值形式：![image-20220303222106717](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220303222106717.png)

     **注意**：使用np.string_类型时，要小心，因为Numpy的字符串数据是大小固定的，发生截取时不会发出警报

***

## Numpy数组运算

​       Numpy用户将数组成为矢量化

* 大小相同的数组之间的任何算术运算都会将运算应用到元素级（元素级别的运算）
* 数组与标量的算术运算会将标量传播到各个元素（即标量会与数组内的每个元素运算）
* 同型数组之间比较会生成**布尔型数组**
* 不同大小的数组之间的运算叫做广播

### 数组转置与轴对换

​         Numpy数组转置，均是**对原数组**进行转置，**不会生成新数组.** 矩阵转置是在进行矩阵计算时经常要用到的操作

* transpose方法：该方法有着特殊的转置原理，但对二维数组在没有其它参数的情况下默认为转置
  * 对于**高维数组**，transpose需要一个**由轴编号**组成的**元组**才能进行转置
* T属性
  * 基本形式：arr.T
* swapaxes方法：也需要一对轴编号



***

## 基本索引和切片

***

### 基本索引

​	Numpy数组的切片与Python的列表切片最重要的**区别**在于：

* 对Numpy的切片数组的元素进行修改，这种修改同时也会发生在原数组中

* 而Python的列表切片不会改动原列表![image-20220304160143891](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220304160143891.png)![image-20220304160155144](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220304160155144.png)

* 切片 [ : ]会给**数组中的所有元素**赋值，因为省略了start和stop，就默认从头到尾![image-20220304160524092](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220304160524092.png)

* 当我们面对二维及以上的数组时，我们的索引有两种方式

  * 一：arr [x] [y] [z]....![image-20220304161109139](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220304161109139.png)

  * 二：arr [x,y,z,.....]

    ![image-20220304161120999](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220304161120999.png)

  * 二维数组的索引方式示意图![image-20220304162603334](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220304162603334.png)

  * 三维数组的排列方式

***

### 切片索引

* ndarray的切片语法和Python一维列表差不多

  * 一维数组：arr [ start : stop ]，start和stop均可以省略，省略则表示从头开始或一直到尾部

  * 多维数组：arr [start:stop（行）, start:stop（列）, ......]

    ![image-20220304163452976](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220304163452976.png)
    
  * 多维数组索引示意图，包含行与列的索引![image-20220304163758507](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220304163758507.png)
  
  * 自然，对切片表达式的赋值操作也会被扩散到整个选区

***



### 布尔值索引

​      在Numpy中，跟算术运算一样，数组的比较运算（如==）也是矢量化的。**布尔型索引是一种经常要用到的手段**

1. 我们可以通过 字符串 和 字符串数组 的比较得到**布尔型数组**![image-20220304165723668](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220304165723668.png)

   ![image-20220304165710060](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220304165710060.png)

* 这个布尔型数组可以用于**数组索引**![image-20220304165846653](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220304165846653.png)

  会将对应布尔值为True的那一行提取出来

* 还能索引行![image-20220304170011063](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220304170011063.png)

* 当我们要取数 'Bob' 以外的其他值，既可以使用（**！=**）也可以使用（**~**）对条件进行反转![image-20220304170156616](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220304170156616.png)

* 通过布尔型索引选取数组中的元素，将总是创建数据的副本

* **注意！！**：**Python关键字and和or在布尔型数组中无效，要使用 & 与 |**

*  利用布尔型索引设置值是一种经常要用到的手段。如下我们要将data数组中所有的负值设置为0![image-20220304205043531](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220304205043531.png)



***

### 花式索引

Numpy的术语，指的是利用 **整数数组** 进行索引

* 我们先创建一个8*4的数组![image-20220304205606004](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220304205606004.png)

* **为了以特定的顺序选取子集**，只需传入一个**用于指定顺序**的**整数列表**或**ndarray数组**即可![image-20220304205808738](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220304205808738.png)

  如果用此方法，是用**负数索引**将会**从末尾**开始选取行![image-20220304210201647](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220304210201647.png)

* 当我们一次传入多个索引数组时，不同的索引数组之间对应位置的各个索引会组合为一个位置坐标，这个位置坐标代表了被索引数组内元素的位置，所有坐标的元素被索引出来组成一个一维数组![image-20220304210910226](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220304210910226.png)

***

## 通用函数(ufunc) 

​         快速的元素级数组函数

**通用函数（ufunc）**是一种对ndarray中的数据执行**元素级运算**的基本函数。我们可以把它看成是一些经过**矢量化包装**之后的简单函数

**矢量化**是指用**数组表达式替换显式的for循环（即用数组表达式代替循环的做法）**，在Python中循环数组或其他跟数组类似的数据结构时，使用循环会涉及很多开销。 NumPy中的矢量化操作把内部循环委托给高度优化的C和Fortran函数，从而实现更清晰，更快速的Python代码。

许多ufunc都是简单函数变体，如sprt和exp![image-20220304222909110](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220304222909110.png)

***

### np.sqrt():

  对数组内的**每个元素**开方（元素级运算），**一元（unary）：只接受一个数组**

***

### np.exp()

   对数组内**每个元素**算e的指数函数，一元。

***

### np.maximum()

​    二元（binary），**接受两个同型数组**，并对两个数组对应位置的元素进行比较，将大的一个作为新数组的元素，最终输出每个位置最大元素组成的数组

***

### 其余常见一元ufunc

![image-20220305105242877](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220305105242877.png)![image-20220305105303123](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220305105303123.png)![image-20220305105415200](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220305105415200.png)

### 二元ufunc

   如常见的四则运算，比较以及逻辑运算等，同样是元素级别的运算

![image-20220305105655084](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220305105655084.png)![image-20220305105705984](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220305105705984.png)

***

## 利用数组进行数据分析

Numpy数组是我们可以将许多数据处理任务表述为简洁的数组表达式（否则需要编写循环），用数组表达式代替循环的做法就是矢量化。一般来说，矢量化数组运算要比等价的纯Python代码快上一两个数量级，尤其是数值计算。

### np.meshgrid(  )

​     生成坐标矩阵，函数接受两个一维数组，分别作为行/列向量，返回值为两个坐标矩阵（X,Y），X中储存的是所有点的横坐标，Y中的是纵坐标，X，Y对应位置元素组合为一个坐标点

![image-20220305111729977](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220305111729977.png)![image-20220305111741749](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220305111741749.png)![image-20220305112004773](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220305112004773.png)

y矩阵中的行代表位于同一纵坐标的点，他们在x矩阵中大的值增大，即代表了是从左向右

***

### 将条件逻辑表述为数组运算

1.  **np.where( c , x , y )** :三元表达式 x if c else y的矢量化版本

    假设我们要根据cond中的值选取xarr和yarr的值时，当cond中的值为True时，选取xarr，若为False时，则选yarr![image-20220305113713950](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220305113713950.png)

   * 纯Python操作（用列表推导式）![image-20220305113727820](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220305113727820.png)

   * np.where( c, x, y)![image-20220305113828784](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220305113828784.png)

   * 纯Python的操作有几个问题，第一，他对大数组大的处理速度慢。第二，无法用于多维数组。而np.where可以，且更简单

   * np.where的 第二个 和第三个参数不必是数组（第一个是条件判断），他们都可以是标量。

     例如我们想将一个随机数组中所有的正值替换为2，所有的负值换为-2![image-20220305114655053](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220305114655053.png)

     当然还有另一种方法（布尔型索引）麻烦一点![image-20220305114913287](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220305114913287.png)

***



### 数学与统计方法

​        可以通过数组上的一组数学函数对整个数组或某个轴向的数据进行统计计算。sum、mean以及标准差std等聚合计算（aggregation，通常叫做约简（reduction）），既可以当做数组的实例方法调用，又可以当作顶级Numpy函数使用

1. **mean **: 求**平均值**

   * array.mean()

   *  np.mean(array)
   * mean函数经常操作的参数是**axis**，以m*n的矩阵为例：
     * 当axis不设置值时，默认对数组内所有的元素（m*n个元素）求平均值；
     * axis=0：压缩行，对各列求均值，返回1*n的矩阵
     * axis=1：压缩列，对各行求矩阵，返回m*1的矩阵

2. **sum**：求和

   * 其用法与mean相同，两种调用形式，axis参数

3. **cumsum方法**：逐位累加函数，累加的结果作为相应位置的元素

   * 也是两种调用形式
   * axis参数，axis=0为行累加，axis=1为列累加，一般要设置axis参数，否则默认是行累加
   * 不会聚合为一个值

4. **cumprod方法**：逐位累乘，累乘的结果作为相应位置的元素

   * 用法与cumsum相同

5. 全部的基本数组统计方法。

   ![image-20220305135855392](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220305135855392.png)![image-20220305135920542](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220305135920542.png)

***



### 用于布尔型数组的方法

在数组统计方法中，布尔值会被强制转换为1（True）和0（False）。因此，sum经常被用来对布尔型数组中的True值计数![image-20220305140250323](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220305140250323.png)

* **any方法**：测试数组中是否存在一个或多个True，但首先得先有布尔型数组
* **all方法**：检查数组中所有值是否都为True![image-20220305140632781](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220305140632781.png)

***

### 排序

​      跟Python内置的列表一样，Numpy的数组也可以通过 **sort方法**就地排序

1. **array.sort()**

* 调用方式：array.sort()![image-20220305141102124](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220305141102124.png)
* 注意：调用之后会修改原数组
* **多维数组可以沿着任何一个轴向上进行排序**，只需要将轴编号传给sort即可（即**沿x轴正方向**进行排序或**沿y轴正方向**排序，每一行或列都会按这个指定顺序排列）![image-20220305141225359](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220305141225359.png)

2. **np.sort(arrray,axis)**
   * 操作与array.sort()基本相同
   * 区别在于：array.sort()是对原数组进行修改，而顶级方法np.sort()返回的是已排序的副本，不会对原数组进行操作



***

### 唯一化以及其他的集合逻辑

​    Numpy提供了一些针对**一维ndarray**的基本集合运算，最常用的可能要数np.unique()了

1. **np.unique(arr)**:
   * 作用：将数组中一些重复出现的元素进行唯一化(即删去重复的，只留下一个)，同时返回**已排序**好的结果![image-20220305143416557](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220305143416557.png)
2. **np.in1d(arr1, arr2)**
   * 用途：用于测试一个数组arr1中的值在另一个数组arr2中是否存在，返回一个**布尔型数组**（大小与arr1相同）![image-20220305143831172](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220305143831172.png)
3. 其他NumPy的集合函数![image-20220305143910703](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220305143910703.png)

***

## 线性代数

​     线性代数（如矩阵乘法、矩阵分解、行列式以及其他方阵数学等）是任何数组库的重要组成部分

### 矩阵乘法

  dot点积

1. **array_x.dot(array_y)**:相当于 矩阵x 左乘 矩阵y，![image-20220305145213560](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220305145213560.png)

2. **np.dot(array_x,  array_y )**

   x.dot(y)等价于np.dot(x, y), **注意矩阵乘法的顺序**

3. **@**符（类似Python3.5）也可以用作**中缀运算符**![image-20220305145903636](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220305145903636.png)

   

   * 中缀运算符：我们日常使用的运算符就是中缀运算符，中缀表达式就是指运算符在运算数中间的表达式

4. 一些最常用的线性代数函数

   ![image-20220305150044559](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220305150044559.png)

## 伪随机数生成

​     np.random对Python内置的random进行了补充增加了一些用于高效生成多种概率分布样本值的函数

​    我们说的这些都是伪随机数，因为他们都是通过算法基于随机数据生成器种子，在确定性的条件下生成的。

1. **numpy.random.normal(loc=0.0, scale=1.0, size=None)**
   * 功能：从正态（高斯）分布中抽取随机样本
   * 参数：
     * loc：分布的均值（中心）
     * scale：分布的标准差（宽度）
     * size：生成数组的大小![image-20220305155206204](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220305155206204.png)
2. **np.random.seed()**: 更改随机数种子![image-20220305155112093](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220305155112093.png)

3. numpy.random的**数据生成函数**使用了**全局的随机种子**。要避免全局状态，你可以使用numpy.random.RandomState，创建一个与其它隔离的随机数生成器：![image-20220305155125873](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220305155125873.png)
4. np.random中的部分函数![image-20220305155258794](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220305155258794.png)![image-20220305155315605](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220305155315605.png)



6. **numpy.random.rand(d0,d1,..,dn )**

* rand函数 根据给定维度生成[0,1)之间的随机数据，包括0，不包括1
* dn 表示每个维度
* 返回值为**指定维度的array**

7. **numpy.random.randn(d0,d1,d2,...,dn)**

* randn函数返回一个或一组样本，具有标准正态分布
* dn表示每个维度
* 返回值为指定维度的array

8. **numpy.random.randint(low, high=None, size=None, dtype='/')**

* 返回**随机整数**，范围区间为[low,high), 包含low, 不包含high
* 参数：low为最小值，high为最大值，size为数组维度大小，dtype为数据类型，默认的数据类型为np.int
* high没有填写时，默认生成随机数的范围是[0,low)

