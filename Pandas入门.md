# Pandas入门

* Pandas含有使数据清洗和分析工作变得更简单的数据结构和操作工具，pandas经常和其它工具一同使用，如数值计算工具NumPy和SciPy，分析库statsmodels和scikit—learn，和数据可视化库matplotlib。Pandas是基于NumPy构建的，特别是基于数组的函数和不使用for循环的数据处理
* Pandas和NumPy最大的不同在于pandas是专门为**处理表格**和**混杂数据**设计的。而NumPy**更适合处理数值数组数据**

***

## Pandas数据结构

### Series

1. Series是一种类似于一维数组的对象，他由一组数据（各种NumPy数据类型）以及一组与之相关的数据标签（或索引）组成。仅由一组数据即可产生最简单的Series：![image-20220305203636763](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220305203636763.png)

   * 本质：相当于表格中的一列
   * 函数：pandas.Series( data, index, dtype, name, copy)
     * data：一组数据（即ndarray对象）
     * index：数据索引标签，如果不指定，默认从0开始
     * dtype：数据类型，默认系统自己判断
     * name: 设置名称
     * copy：拷贝数据，默认为False
   * 属性：Series.values可以查看值，Series.index可以查看索引
   * 表现形式：索引在左边，值在右边

2. **索引**

   我们希望指定每个数据的索引![image-20220305205137925](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220305205137925.png)

   * 与普通NumPy数组相比，我们可以通过索引的方式选取一个Series中的单个或一组值![image-20220305205612537](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220305205612537.png)

      ['b', 'c', 'd']是索引列表，即使它包含的是字符串而不是整数

   * Series的索引可以通过**赋值**直接**就地修改**![image-20220305212555722](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220305212555722.png)

     

   * 还可以把Series看成是一个定长的有序字典，因为他是**索引值到数据值**的一个**映射**。它可以用在许多需要字典参数的函数中![image-20220305210516567](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220305210516567.png)

   * 我们还可以用Python的**字典来创建Series**：![image-20220305211119137](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220305211119137.png)

     如果只传入一个字典，则结果Series中的索引就是原字典的键（有序排列）。你可以在index参数处**额外传入**排好序的字典的键以改变顺序![image-20220305211616966](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220305211616966.png)

     在这个例子中，由于’California‘的字符串在原字典的键中找不到匹配值，所以它所对应的为**NaN**（即“非数字”：Not a Number），在pandas中，它用于表示**缺失**或**NA值**

   * pandas的**isnull**和**notnull**函数可用于**检测缺失数据**![image-20220305212124825](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220305212124825.png)

     Series对象也有一样的方法：Series.isnull![image-20220305212256533](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220305212256533.png)

***



### DataFrame

​       DataFrame是一个**表格型**的数据结构，它含有一组有序的列，每列可以是不同的值类型（数值，字符串，布尔值）。DataFrame既有行索引也有列索引，它可以被看成由Series组成的字典（共同用一个索引）![image-20220305213558303](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220305213558303.png)![image-20220305213747638](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220305213747638.png)

1. ```
   pandas.DataFrame( data, index, columns, dtype, copy)
   ```

* 参数：
  * data:一组数据 （ndarray，series，map，lists，dict等类型）
  * index：索引值，或者可以成为行标签
  * columns: 列标签
  * dtype：数据类型
  * copy：拷贝数据默认为False

2. DataFrame创建方法：最常用的创建方法是直接传入一个由**等长列表**作为值的**字典**

   * 最常用的创建方法：![image-20220306102654938](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306102654938.png)

   * **指定列标签序列（columns）**，DataFrame的列标签就会按照指定顺序进行排列![image-20220306103534485](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306103534485.png)

     如果传入的列在数据中找不到，就会在结果中产生缺失值：![image-20220306103913089](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306103913089.png)

   * **指定行标签（index）**![image-20220306104020346](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306104020346.png)

   * DataFrame所能接受的所有数据![image-20220306151023310](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306151023310.png)



3. **head方法**：对于特别大的DataFrame，head方法会选取前五行进行展示![image-20220306103142608](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306103142608.png)

4. **索引**：

   * **整列索引**：可以通过类似字典的key的或属性的方式，获取DataFrame中的一个Series（DataFrame中的每一列就是一个Series）：

     * 用key：![image-20220306104343391](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306104343391.png)
     * 用**属性的调用方式**索引列：![image-20220306104404478](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306104404478.png)
     * 注意，返回的Series拥有原DataFrame相同的索引，且其name属性已经被相应地设置好了

   * **整行索引**：行也可以通过位置或名称的方式进行获取，比如说loc属性![image-20220306104930795](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306104930795.png)

     **注意行索引时要用.loc的方法才行，否则会与列索引的一种方式冲突**

5. **赋值**：赋值操作可以在索引的基础上进行（先索引才能赋值）

   * **对行列赋值**

     ![image-20220306131043715](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306131043715.png)

   * **将列表或者数组赋值给DataFrame某个列**时：

     其长度必须跟DataFrame的长度相匹配。如果赋值的是一个Series，就会根据Series内的索引精确地匹配DataFrame的索引。![image-20220306131606265](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306131606265.png)

     如果是为一个**不存在的列**赋值，DataFrame会**创建出一个新列**

     我们可以用类似字典key的索引方式来创建新的列，但是不能用查看属性的方式frame2.eastern创建新的列

   * **嵌套字典赋值**

     ![image-20220306145821366](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306145821366.png)

     如果**嵌套字典**传给DataFrame，pandas就会将其解释为：**外层字典的键**作为**列索引**，**内层键**则作为**行索引**：![image-20220306150148145](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306150148145.png)

     如果我们已经明确地指定了索引，那么最终会按我们的指定的索引生成DataFrame![image-20220306150642242](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306150642242.png)

   

6. **删除列**

* **关键字del用于删除列**![image-20220306132142484](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306132142484.png)
* **注意**：如果我们在对DataFrame进行操作时不进行copy，那么对Series所做的任何修改全都会修改到原DataFrame中。

7. **转置**：用类似NumPy数组的方法，对DataFrame进行转置（交换行和列）：
   * frame.T![image-20220306151051304](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306151051304.png)

8. **DataFrame属性**：
   * 设置**index**和**columns**的**names属性**，这些信息也会被显示出来：![image-20220306151411278](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306151411278.png)
   * **values属性**：DataFrame.values属性会以二维的ndarray返回数据![image-20220306151726403](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306151726403.png)
   * 如果DataFrame割裂的数据类型不同，则数组的dtype就会选用能兼容所有列的数据类型

### 索引对象

​     pandas的索引对象负责管理轴标签和其他元数据（比如轴名称），构建Series或DataFrame时，所用到的任何数组或序列的标签都会被转换成一个index![image-20220306152306063](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306152306063.png)

* index对象内部的值是不可变的、不可被赋值的，这种不变性可以使index对象在多个数据结构之间安全共享（即我们可以先创建一个Index对象，再用他来创建Series或DataFrame）![image-20220306152959709](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306152959709.png)
* Index的功能类似于固定大小的集合，可以用in查询，也可以含有重复的标签
* ![image-20220306153221043](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306153221043.png)



## 基本功能

### 重新索引

1. **reindex方法**：根据我们**指定的新索引**进行**重排**，如果某个索引值不存在，就先创建再引入缺失值
   * 基本使用：填入我们想要的index顺序![image-20220306153813705](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306153813705.png)
   * **插值处理**：对于时间序列这样的有序数据，重新索引使可能需要做一些插值处理。**method选项**可以做到。如利用ffill实现向前插值![image-20220306154140187](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306154140187.png)
   * 修改**DataFrame的行索引**![image-20220306154636394](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306154636394.png)
   * 修改**DataFrame列索引**：只需要用reindex中的columns选项即可![image-20220306154833921](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306154833921.png)
   * reindex函数**参数**![image-20220306154940733](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306154940733.png)



### 丢弃指定轴上的项

​    利用**drop方法**可以删除一个指定轴上的指定值

* 删除**行（默认axis = 0）**![image-20220306155444266](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306155444266.png)

  

* 删除**列（axis = 1或axis = 'columns'）**：

* **删除某行或列的所有**：**inplace选项（inplace=True）**![image-20220306160429272](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306160429272.png)

  小心使用inplace，他会销毁所有被删除的数据

### 索引、选取和过滤

1. **Series索引**：

   ​      Series索引的工作方式类似于NumPy数组的索引，只不过Series的索引**不只是整数，Series的索引方式很多样**

   * 由于Series只有一列，所以**Series的索引对象是行标签**

   * 基本索引：![image-20220306161120498](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306161120498.png)

   * **标签切片索引**：利用标签的切片运算于普通的Python切片运算不同，其末端是包括的![image-20220306161314491](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306161314491.png)

   * 在切片索引的基础上一样可以进行**赋值**![image-20220306161428782](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306161428782.png)

2. **DataFrame索引**

   * 用一个值或序列对DataFrame进行索引其实就是获取一个或多个列：![image-20220306161941924](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306161941924.png)

   * 切片：对行

     ![image-20220306162301660](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306162301660.png)

   * 布尔型索引：先生成布尔型数据再索引，再赋值![image-20220306162440900](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306162440900.png)

     ![image-20220306162543422](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306162543422.png)

   * 用**loc**和**iloc**进行选取：loc和iloc用于对DataFrame的行进行索引：![image-20220306163059797](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306163059797.png)
     * 利用整数先选取行，再选取列![image-20220306163307699](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306163307699.png)
     * **多标签切片**：![image-20220306163733216](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306163733216.png)

   * DataFrame所有索引方式：![image-20220306164135270](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306164135270.png)

   

3. **整数索引**

   * pandas勉强可以进行整数索引，但是会导致小Bug。例如如下Series，虽然内部包含有0，1，2的整数索引，但是**可能会与values冲突**，所以**不推荐将索引设置为整数**

     ![image-20220306164734015](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306164734015.png)

   * 对于非整数 索引，不会产生歧义![image-20220306164842471](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306164842471.png)

   * 为了统一，如果轴索引含有整数，数据选取总会先使用标签。为了更准确，请使用**loc（标签）或 iloc（整数)**(即利用loc和iloc对行索引)：![image-20220306165413107](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306165413107.png)

***

### 算术运算和数据对齐

​         pandas可以对不同索引值的对象进行算术运算，

1. **加**：在将对象相加时，如果存在不同的索引值，则结果的总索引序列就是该索引对的并集

   * Series相加： 自动数据对齐操作，在**不重叠的索引处**引入了NaN值，只要不重叠就是NaN（**注意！！只有行索引 / 行标签一模一样的两个元素才会相加，否则就缺失**）

     ![image-20220306180005494](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306180005494.png)

   * DataFrame相加：两个DataFrame相加后会返回一个新的DataFrame，其索引和列为原来那两个DataFrame的并集：

     （**只有index和columns都对应的两个元素才会相加，否则就缺失**）

     ![image-20220306180844419](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306180844419.png)![image-20220306180853145](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306180853145.png)

     

2. **在算术方法中填充值**：在不同索引的对象中进行算术运算时，你可能希望当一个对象中某个轴标签在另一个对象中找不到匹配轴时填充一个特殊值（比如0）

   * add方法中的 fill_value参数使得缺失的位置会被不匹配的值填充，而不是变为缺失值NaN

     ![image-20220306182258981](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306182258981.png)

   * 与此类似，在对Series或DataFrame重新索引（reindex）时，也可以指定一个填充值![image-20220306182828636](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306182828636.png)

3. **DataFrame和Series之间的运算**：跟不同的NumPy数组一样，DataFrame和Series之间算术运算也是有明确规定的
   * 在NymPy中，一个二维数组以某行做差的操作会传播到每一行，DataFrame和Series之间的运算差不多也是如此![image-20220306191531588](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306191531588.png)
   * 默认情况下，DataFrame和Series之间的算术运算会将Series的索引匹配到DataFrame的列，然后沿着行向下广播：![image-20220306191811061](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306191811061.png)
   * 如果某个索引值在DataFrame的列或Series的索引中找不到，则参与运算的两个对象会被**重新索引**以**形成并集**，匹配不到的索引则被设置为NaN![image-20220306191933422](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306191933422.png)
   * 如果我们希望在行或列上广播，则必须使用算术运算方法![image-20220306192536031](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306192536031.png)

### 函数应用和映射

1. NumPy的ufunc（元素级数组方法）也可以用于操作pandas对象
   * ![image-20220306193032588](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306193032588.png)

2. **apply()方法**：将函数应用到由各列和各行所形成的一维数组上**，DataFrame的**apply（）**方法![image-20220306193544715](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306193544715.png)

* 基本形式： dataframe.apply(function, axis)

* **借助apply方法执行的函数一般是自定义函数**
* 传递到apply的函数不是必须返回一个标量，还可以返会有多个值组成的Series（由自定义函数决定）：![image-20220306194136018](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306194136018.png)

3. **applymap(function)方法**:与apply作用相似，但**applymap是元素级**，**apply只是行列级的**![image-20220306194743306](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306194743306.png)
   * **注意！！applymap( )方法不能用于Series，只属于DataFrame。而Series中的是series.map()**

***

### 排序与排名

​    根据条件对数据集排序（sorting）也是一种重要的内置运算。

1. 排序：

* **sort_index方法**：要**对行索引**或**列索引**进行排序（**注意不是对值排序！！**），可使用**sort_index方法**，他将返回一个已排序的对象：

  * 对Series![image-20220306195416907](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306195416907.png)

  * 对DataFrame，则可以指定**任意一个轴上的索引**进行排序，默认axis=0：![image-20220306195806962](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306195806962.png)

    数据**默认是按升序**排序(ascending=True)的，但也可以降序排序：![image-20220306200018104](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306200018104.png)

* **sort_values方法**：对**值**排序

  * 在排序时，**任何缺失值**都会被放到Series的末尾：![image-20220306200607052](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306200607052.png)
  * 当排序一个DataFrame时，我们可以将一个或多个列的名字传递给sort_values()的by选项，就可以对一个或多个列中的值进行排序:![image-20220306201002991](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306201002991.png)![image-20220306201047720](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306201047720.png)

2. 排名：排名会从1开始一直到数组中有效数据的数量。
   * **rank（）方法**：rank是通过为各组分配一个平均排名的方式破坏平级关系：![image-20220306201620167](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306201620167.png)
   * 也可以结合**值的大小**和**值在原数据中出现的顺序**给出排名（避免了平级）![image-20220306201808595](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306201808595.png)
   * 降序（ascending =False）:![image-20220306202127897](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306202127897.png)
   * 所有用于破坏平级关系的method选项：![image-20220306202418959](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306202418959.png)

### 带有重复标签的轴索引

​          虽然很多pandas函数（如reindex）都要求标签唯一，但这并不是强制性的。如下的带重复标签的Series：![image-20220306202739091](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306202739091.png)

1. **is_unique属性**：这个属性可以**检测唯一性**。可以用在检测索引是否唯一。![image-20220306202953010](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306202953010.png)

   * 对于带有重复值的索引，数据选取将会有些不同。如果某个索引对应多个值，则会返回一个Series：而对应单个值的，则返回一个标量，对DataFrame的行进行索引也是如此。

     

***

## 汇总和计算描述统计

​       pandas对象用一组常用的数学和统计方法，他们大部分都属于**约简**和**汇总统计**，用于从Series中提取单个值（如sum或mean）或从DataFrame的行或列中提取一个Series。跟对应的NumPy数组方法相比，**他们都是基于没有缺失数据的假设而构建的**![image-20220306204042604](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306204042604.png)

1.**sum( )** : 会返回一个求和之后的Series

* 基本使用：![image-20220306204100909](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306204100909.png)

* **axis参数改变求和的方向**：sum()内的axis参数默认为0，即按列求和。axis=1则会按行求和

  ![image-20220306204529831](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306204529831.png)

  ![image-20220306204542390](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306204542390.png)

* NAN值会自动被排除，除非整个切片（这里指的是行或列）都是NAN。通过skipna选项可以禁用该功能![image-20220306204943754](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306204943754.png)
* 约简方法的选项：![image-20220306205052061](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306205052061.png)

2. **idxmin ( )**和 **idxmax( )** 返回的是**间接统计**（比如达到最小值和最大值的索引）：

   ![image-20220306205435203](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306205435203.png)

3. **cumsum（）方法**：累计型方法，累加。

   ![image-20220306205533034](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306205533034.png)

4. **describe( )方法**：用于一次性产生多种统计结果

   * 对数值型数据：![image-20220306205730136](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306205730136.png)
   * 对非数据型数据：![image-20220306205803826](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306205803826.png)
   * 所有与统计相关的方法：![image-20220306210030530](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306210030530.png)

### 相关系数与协方差

​       有些汇总统计（如相关系数和协方差）是通过参数对计算出来的。我们来看几个。

该部分由于pandas_datareader模块的使用出现问题，故没有实践代码

### 唯一值，值计数以及成员资格

1. **unique函数**：可以得到Series中的唯一值数组：![image-20220306212628569](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306212628569.png)
   * 返回的唯一值是未排序的，如果需要的话，可以对结果再次进行排序（unique.sort()）

2. **value_counts()**: 计算一个Series中**各值出现的频率**，**pandas顶级方法**，可以用于**任何数组**或**序列**：

   ![image-20220306213123407](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306213123407.png)

3. **isin()方法**：用于查询矢量化集合大的成员资格，即与Python的in差不多，最终生成布尔型数据

   ![image-20220306213832561](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306213832561.png)

   

4. **Index.get_indexer()**方法：Index对象内部的一种方法![image-20220306215024413](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306215024413.png)
5. ![image-20220306215103441](C:\Users\27410\AppData\Roaming\Typora\typora-user-images\image-20220306215103441.png)







 







































