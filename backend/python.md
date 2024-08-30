<!--
 * @Author: zhangmaokai zmkfml@163.com
 * @Date: 2024-02-22 14:57:45
 * @LastEditors: zhangmaokai zmkfml@163.com
 * @LastEditTime: 2024-04-15 16:02:04
 * @FilePath: /记录/Coder/backend/python.md
 * @Description: python学习速记
-->
# Python速记
1. 像.exe文件那样在mac和linux上直接运行python文件，第一行加一个特殊的注释；第二行表示使用标准UTF-8编码
```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

print('hello, world')
```

2. 简单方法
- 十进制转二进制：bin(dec)
- 转八进制为：oct(dec)
- 转十六进制为：hex(dec)
- 获取字符的整数表示：ord('张')
- 编码转换为对应的字符：chr(24352)
- 列表生成式方便生成数组：list(range(1,10))

由于Python的字符串类型是str，在内存中以Unicode表示，一个字符对应若干个字节。如果要在网络上传输，或者保存到磁盘上，就需要把str变为以字节为单位的bytes。
```python
# 以Unicode表示的str通过encode()方法可以编码为指定的bytes：
'ABC'.encode('utf-8') => 输出 b'ABC' 
```
反过来，如果我们从网络或磁盘上读取了字节流，那么读到的数据就是bytes。要把bytes变为str，就需要用decode()方法
```python
b'\xe4\xb8\xad\xe6\x96\x87'.decode('utf-8') => 输出'中文'
```
如果bytes中只有一小部分无效的字节，可以传入errors='ignore'忽略错误的字节：
```python
b'\xe4\xb8\xad\xff'.decode('utf-8', errors='ignore') => 输出'中'
```
一个中文字符通过UTF-8编码后占3个字节、而一个英文字符占1个字节

3. 列表生成式
举个例子，要生成list [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]可以用`list(range(1, 11))`
但如果要生成[1x1, 2x2, 3x3, ..., 10x10]怎么做？列表生成式则可以用一行语句代替循环生成上面的list：
```python
[x * x for x in range(1, 11)] =>输出[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```
for循环后面还可以加上if判断，这样我们就可以筛选出仅偶数的平方
```python
[x * x for x in range(1, 11) if x%2==0] =>输出[4, 16, 36, 64, 100]
```
把一个list中所有的字符串变成小写
```python
L = ['Hello', 'World', 'IBM', 'Apple']
[s.lower() for s in L]
=> 输出['hello', 'world', 'ibm', 'apple']
```
测试通过如下例子：
```python
# 测试:
print(L2)
if L2 == ['hello', 'world', 'apple']:
    print('测试通过!')
else:
    print('测试失败!')

# 解答
L1 = ['Hello', 'World', 18, 'Apple', None]
L2 = [x.lower() for x in L1 if isinstance(x,str)]
=> 输出['hello','world','apple']
```

4. map/reduce
map()函数接收两个参数，一个是函数，一个是Iterable，map将传入的函数**依次作用到序列的每个元素**，并把结果作为新的Iterator返回。
```python
>>> def f(x):
...     return x * x
...
>>> r = map(f, [1, 2, 3, 4, 5, 6, 7, 8, 9])
>>> list(r)
[1, 4, 9, 16, 25, 36, 49, 64, 81]
```
reduce把一个函数作用在一个序列[x1, x2, x3, ...]上，这个函数必须接收两个参数，reduce把**结果继续和序列的下一个元素做累积计算**
```python
>>> from functools import reduce
>>> def fn(x, y):
...     return x * 10 + y
...
>>> reduce(fn, [1, 3, 5, 7, 9])
13579
```

5. filter
和map()类似，filter()也接收一个函数和一个序列。和map()不同的是，filter()把传入的函数依次作用于每个元素，然后**根据返回值是True还是False决定保留还是丢弃该元素**。
```python
# 例如，在一个list中，删掉偶数，只保留奇数，可以这么写：

def is_odd(n):
    return n % 2 == 1

list(filter(is_odd, [1, 2, 4, 5, 6, 9, 10, 15]))
# 结果: [1, 5, 9, 15]
```