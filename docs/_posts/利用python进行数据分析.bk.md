---
title: 利用Python进行数据分析
date: 2019-08-10 14:15:42
tags:
---

## 第 1 章 准备工作

### 1.1 本书内容

#### 1.1.1 什么类型的数据

### 1.2 为何利用 Python 进行数据分析

#### 1.2.1 Python作为胶水

#### 1.2.2 解决“双语言”难题

#### 1.2.3 为何不使用 Python

### 1.3 重要的 Python库

## 第 2 章

## 第 3 章

## 第 4 章

## 第 5 章

### 5.1

#### 5.1.1

#### 5.1.2

#### 5.1.3 索引对象

表5-2：一些索引对象的方法和属性

|方法|描述|
|:--|:--|
|append|将额外的索引对象粘贴到原索引后，产生一个新的索引|
|difference|计算两个索引的差集|
|intersection|计算两个索引的交集|
|union|计算两个索引的并集|
|isin|计算表示每一个值是否在传值容器中的布尔数组|
|delete|键位置i的元素删除，并产生新的索引|
|drop|根据传参删除指定索引值，并产生新的索引|
|insert|在位置i插入元素，并产生新的索引|
|is_monotonic|如果索引序列递增则返回True|
|is_unique|如果索引序列唯一则返回True|
|unique|计算索引的唯一值序列|

## 第 6 章 数据载入、存储及文件格式

### 6.1 文本格式数据的读写

#### 6.1.1

#### 6.1.2

#### 6.1.3

#### 6.1.4

#### 6.1.5

### 6.2 二进制格式

#### 6.2.1 使用 HDF5 格式

```python
 df.to_hdf('./x.h5','key')
 pd.read_hdf('./x.h5','key')
```

#### 6.2.2 读取Microsoft Excel 文件

excel操作

```python
pandas.read_excel（io，sheet_name = 0，header = 0，names = None，index_col = None，usecols = None，squeeze = False,dtype = None, ...）
#io:文件路径
#sheet_name:sheet_name=0,sheet_name=“Sheet1”,sheet_name=[0,1,'Sheet5']
#header：指定作为列名的行,默认0，即取第一行的值为列名。数据为列名行以下的数据；若数据不含列名，则设定 header = None。
#names：默认为None，要使用的列名列表，如不包含标题行，应显示传递header=None。
#index_col：指定列为索引列，默认None列（0索引）用作DataFrame的行标签。
#usecols：int或list，默认为None。
##如果为None则解析所有列
##如果为int则表示要解析的最后一列
##如果为int列表则表示要解析的列号列表
##如果字符串则表示以逗号分隔的Excel列字母和列范围列表（例如“A：E”或“A，C，E：F”）。范围包括双方。
#squeeze：boolean，默认为False,如果解析的数据只包含一列，则返回一个Series。
#skiprows：省略指定行数的数据,从第一行开始。
#skipfooter：省略指定行数的数据，从尾部数的行开始。
#dtype:字典类型{'列名1':数据类型，‘列名’:数据类型}，设定指定列的数据类型。
```

### 6.3 与Web API 交互

### 6.4 与数据库交互

数据库操作

```python
engine=create_engine("mysql+pymysql://root:password@127.0.0.1:3306/<sqldata>?charset=utf8",pool_timeout=30) #连接数据库  pool_timeout：连接超时 sqldata:数据库名称
pd.read_sql('select * from <sqldata>',engine,index_col='a') #读取数据库 index_col：索引列 <sqldata>:数据库表名
con = engine.connect() #创建数据库指针
pd.to_sql(name='sqldata', con=con, if_exists='append', index=False)
#name:输出表名
#con: 数据库连接
#if_exists：操作方式（fail:若表存在，则不输出,replace：若表存在，覆盖原来表里的数据append：若表存在，将数据写到原表的后面）
#index:是否将df的index单独写到一列中(False,True)
#index_label:指定列作为df的index输出，此时index为True
#dtype: 指定列的输出到数据库中的数据类型。字典形式储存：{column_name: sql_dtype}。常见的数据类型有sqlalchemy.types.INTEGER(), sqlalchemy.types.NVARCHAR(),sqlalchemy.Datetime()等，具体数据类型可以参考http://docs.sqlalchemy.org/en/latest/core/type_basics.html#sql-standard-and-multiple-vendor-types
engine.dispose() #关闭连接
```

### 6.5

## 第 7 章 数据清洗与准备

### 7.1 处理缺失值

```python
df.a.isnull() #使用isnull 过滤缺失值
```

表7-1：NA处理方法

|函数名|描述|
|:--|:--|
|dropna|根据每个标签的值是否是缺失数据来筛选轴标签，并根据允许丢失的数据量来确当阈值|
|fillna|用某些值填充缺失的数据或使用插值方法（如'ffill'或'bfill'）|
|isnull|返回表明哪些是缺失值的布尔值|
|notnull|isnull的反函数|

#### 7.1.1 过滤缺失值

```python
df.dropna() #默认删除包含缺失值的行 使用how='all'参数删除所有值均为NA的行，使用axis=1删除列，thresh参数可以设定允许缺失值的阈值
```

#### 7.1.2 补全缺失值

表7-2：fillna函数参数

|参数|描述|
|:--|:--|
|value|标量值或字典型对象用于填充缺失值|
|method|插值方法，如果没有其它参数，默认是'ffill'|
|axis|需要填充的轴，默认axis=0|
|inplace|修改被调用的对象，而不是生成一个对象|
|limit|用于前向或者后向填充时最大的填充范围|

### 7.2 数据转换

#### 7.2.1 删除重复值

#### 7.2.2 使用函数或映射进行数据转换

## 第 8 章 数据规整：连接、联合与重塑

### 8.1

#### 8.1.1

#### 8.1.2 按层级进行汇总统计

```python
df.sum(level=0) #使用层级进行汇总
df.sum(level='索引名',axis=1)
```

#### 8.1.3 使用 DataFrame 的列进行索引

```python
df.set_index('A') #使用A列作为索引
df.set_index(['A','c']) #使用A,C列进行分层索引
#使用drop=False参数，可以使作为索引的列保留在DataFrame中
#reset_index是set_index的反函数
```

### 8.2 联合与合并数据

#### 8.2.1 数据库风格的 DataFrame 连接

```python
pd.merge(df1,df2,on='key') #可以分别指定列名left_on='lkey',right_on='rkey' 可使用参数how=
```

表8-1：how 参数的不同连接类型

|选项|行为|
|:--:|:--|
|'inner'|只对两张表都有的键的交集进行联合|
|'left'|对所有左边的键都进行联合|
|'right'|对所有右表的键都进行联合|
|'outer'|对两张表都有的键的并集进行联合|

表8-2：merge函数参数

|参数|描述|
|:-|:-|
|left|合并时操作中左边的DataFrame|
|right|合并时操作中右边的DataFrame|
|how||
|on||
|left_on||
|right_on||
|sort||
|suffixes||
|copy||
|indicator||

#### 8.2.2 根据索引合并

```python
pd.merge(df1,df2,on='key'，right_index=True)
#可以分别指定列名left_on='lkey',right_on='rkey' 可使用参数how=
#可以传递left_index=True或tight_index=True(或者都传)来表示索引需要用来作为合并的键
```

#### 8.2.3

#### 8.2.4

## 第 9 章 绘图与可视化

### 9.1 简明 matplotlib API 入门

```python
%matplotlib inline #用于在juputer notebook中显示图形
```

#### 9.1.1 图片与子图

#### 9.1.2

#### 9.1.3

#### 9.1.4

#### 9.1.5 将图片保存到文件

表9-2：figure.savefig选项

|参数|描述|
|:--|:--|
|fname|包含文件路径或Python文件型对象的字符串。图片格式是从文件的扩展名中推断出来的（例如PDF格式的.pdf或PNG格式的.png格式）|
|dpi|每英寸点数的分辨率；默认为100，但可以配置|
|faceclor,edgecolor|子图之外的图形背景的颜色；默认情况下是'w'（白色）|
|format|文件格式('png','pdf','svg','ps','eps'……)|
|bbox_inches|要保存的图片范围；如果传递'tight'，将会去除掉图片周围空白的部分|

#### 9.1.6

### 9.2 使用 pandas 和 seaborn 绘图
