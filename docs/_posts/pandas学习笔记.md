---
title: Pandas学习笔记
date: 2019-08-10 21:39:18
tags: pandas 
---
**数据库操作**
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
**excel操作**
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
**对于时间序列的一些操作**
```python
import pandas as pd
x=pd.DataFrame({'date':['2016-01-20','2016-01-30','2016-02-25','2016-03-05']},index=['a','c','b','a'])
x['date']=x['date'].astype('datetime64') #转换数据类型
x['date'].dt.week #计算第几周
pd.Timestamp.now() #现在时间
pd.Timedelta(days=4) #创建一个时间长度
pd.Timestamp('2019-08-15') #创建一个时间
```
**索引**
```python
df['a']  #默认为列索引
df.loc['a'] #行索引
df.iloc[2] #行索引
df.loc[:,'a'] #列索引
df.loc[df.A=1,'a'] #布尔索引行后索引列
df[df.a.isin(s)] #索引a列中含s数据的行
df[~df.a.isin(s)] #索引a列中不含s数据的行
df.reset_index() #还原索引
df.columns=['a','b'] #重新命名列索引
df.index=['a','b'] #重新命名行索引
df.drop(['a']) #删除行，使用axis=1参数，删除列
df.a.unique() #唯一值

```
**多层索引**
```python
import pandas as pd
arrays = [[1, 1, 2, 2], ['red', 'blue', 'red', 'blue']]
x=[1,2,3,4]
y=pd.MultiIndex.from_arrays(arrays,names=['num','c']) #
pd.MultiIndex.from_product([["A","B"],['x1','y1']],names=["class1","class2"]) #从笛卡尔积创建Multilndex对象
pd.DataFrame(x,y).T
```
**分组**
```python





```
**DataFrame连接**
```python
df1=pd.DataFrame({'款号':['818009'],'数量':[20]})
df2=pd.DataFrame({'款号':['818009'],'大类':['xx'],'小类':['cc']})
pd.merge(df2,df1,on='款号')
```
**操作元素**
```python
a=lambda a: a.upper()
df['x']=df['x'].map(a)
df=df.applymap(a) #操作每个元素
df=df.apply(a) #操作一行或者一列（使用参数 axis）

```
**重复数据**
```python
df.duplicated() #重复值的布尔数组
df.drop_duplicates() #删除重复值

```


