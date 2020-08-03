# 零散方法和函数收集
## 内置函数
### int()
int(x, base=10)
功能：将字符串或数字转换为整型
parameters：
* x: 字符串或数字
* base: 进制，默认十进制
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