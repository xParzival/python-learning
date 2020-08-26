# 零散方法和函数收集
## 内置函数
### int()
int(x, base=10)
功能：将字符串或数字转换为整型
parameters：
* x: 字符串或数字
* base: 进制，默认十进制
  
### dict.fromkeys(seq[, val])
功能：创建一个新字典，以序列 seq 中元素做字典的键，value 为字典所有键对应的初始值，value没有时默认为None
## numpy
### numpy.vectorize()
numpy.vectorize(pyfunc, otypes=None, doc=None, excluded=None, cache=False, signature=None)
功能：将函数向量化
Parameters:
* pyfunc: python函数或方法
* otypes: 输出数据类型。必须将其指定为一个typecode字符串或一个数据类型说明符列表。每个输出应该有一个数据类型说明符
* doc: 函数的docstring。如果为None，则docstring将是 pyfunc.\_\_doc\_\_
* excluded: 表示函数不会向量化的位置或关键字参数的字符串或整数集。这些将直接传递给未经修改的pyfunc
* cache: 如果为True，则缓存第一个函数调用，该函数调用确定未提供otype的输出数
* signature: 广义通用函数签名，例如，(m,n),(n)->(m)用于矢量化矩阵 - 向量乘法。如果提供的话，pyfunc将调用（并期望返回）具有由相应核心维度的大小给出的形状的数组。默认情况下，pyfunc假定将标量作为输入和输出

Returns:
* vectorized :向量化的数组

例程:
```
def myfunc(a, b):
    "Return a-b if a>b, otherwise return a+b"
    if a > b:
        return a - b
    else:
        return a + b
```
```
vfunc = numpy.vectorize(myfunc)
vfunc([1, 2, 3, 4], 2)
```
返回结果
```
array([3, 4, 1, 2])
```
### numpy.delete(arr,obj,axis=None)
功能：删除数组中指定的行或列
Parameters：
* obj：要删除的行或列的索引
* axis：0代表删除行，1代表删除列，None代表先将数组展平后再按索引删除指定元素

## pandas
### dataframe.dropna(axis=0, how='any', thresh=None, subset=None, inplace=False)
功能：删除缺失值
Parameters：
* axis：0/"index"代表删除有缺失值的行，1/"columns"代表删除有缺失值的列
* how：'any'代表有缺失值就删除该行/列，'all'代表所有值缺失时才删除该行/列
* thresh：必须是整数，比如设为n，表示保留至少有n个非缺失值的行/列，可以用来控制缺失值的比例
* subset：array-like的值，代表检查缺失值的行/列子集，默认对所有行/列操作
* inplace：是否直接在当前dataframe操作，为true则没有返回值

Returns：
* 删除缺失值后的dataframe

### series|dataframe.value_counts()
功能：按所有列值出现的频率计数

### pd.concat()
功能：拼接两个series或dataframe

### GroupBy.agg()
功能：对goupby后的对象使用聚合函数，series和dataframe都有效

### dataframe.convert_types()
功能：转换列的类型