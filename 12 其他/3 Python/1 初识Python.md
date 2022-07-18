# Python

## 语言特点

- 以缩进来控制代码运行（1 个 tab = 4 个空格）

## 注释

```python
# -*- coding: utf-8 -*-  # 编码设置
# 单行注释
'''
多行注释
'''
```

## 变量声明

```python
a = None  # 变量必须进行赋值，可用 None 来占位
b, c, d = 1, 2, 3  # 多个变量赋值
```

### 变量交换

```python

a, b = 1, 2
a, b = b, a
print(a, b)  #--> 2 1
```

## 数据类型

### 数字：

```python
num1 = 123  # 整数型，没有取值范围限制
num2 = 12.3  # 浮点数字类型，浮点数数值范围存在限制，跟不同的计算机系统有关
num3 = 3 + 1j  # 复数
pow(2, 2)  #--> 4

0b10  #--> 2  二进制
0o45  #--> 37  八进制
0x9a  #--> 154  十六进制
bin(10)  #--> 0b1010  转为二进制
oct(10)  #--> 0o12  转为八进制
hex(10)  #--> 0xa  转为十六进制

9e4  #--> 90000.0  9 乘以 10 的 4 次方
num4 = 10e2 + 2j
num4.real  #--> 1000.0  实部
num4.imag  #--> 2.0  虚部

# 运算符
# 加：+  减：-  乘：*  除（返回值为浮点数）：/  除（返回值为整数，向下取整）：//  取余：%  次方：**

# 内置函数
abs(-2)  #--> 2  绝对值
divmod(10, 3)  #--> (3, 1)  求商与余数
pow(3, 2)  #--> 9  3 的 2 次方
round(10.4)  #--> 10  四舍五入
max(1, 3, 2, 8)  #--> 8  最大值
min(1, 3, 2, 8)  #--> 1  最小值
```

- 0.1 + 0.2 = 0.30000000000000004

```python
from decimal import Decimal
a = Decimal('0.1')
b = Decimal('0.2')

print(a + b)
```

### 字符串：

``` python
string = 'hello world'
string[0, 3]  #--> hel  字符串剪切

'hello' + 'world'  #--> helloworld  字符串拼接
'hello' * 2  #--> hellohello

len('hello')  #--> 5  字符串长度
string.upper()  #--> HELLO WORLD  转为大写
string.lower()  #--> hello world  转为小写
string.strip()  # 去除两边空格
string.split(' ')  #--> ['hello', 'world']
```

## type 类型判断

```python
type(123)  #--> init
type(12.3)  #--> float
type(3 + 1j)  #--> complex
type(True)  #--> bool
type(None)  #--> NoneType
```

## 类型转换

```python
int(True)  #--> 1
bool(1)  #--> True
str(10)  #--> 10  字符串类型的 10
```

> 复数不可转为浮点数

## 逻辑运算符

- and ： 与
- or ： 或
- not ： 非

## 帮助

```python
help(None);
```

## id 查看内存地址

```python
a = 3
b = 3
print(id(a), id(b))  #--> 140724775592400 140724775592400  指向同一个地址
```

## eval 运行字符串代码

```python
a, b = 1, 2
eval('a + b')  #--> 3
```

## 条件

```py
num = 2

if num == 1 :
	print('1')
elif num == 2 : 
	print('2')
else :
	print('3')
```

## 循环

### for

```python
string = 'hello'

for prop in string:
    print(prop)
else :  # 这里的 else 表示退出了循环 
    print('循环结束')
#--> h e l l o 循环结束
```

### while

```python
i = 0
while i < 10 :
    print(i)
    i += 1
else :
    print('循环结束')
```

## 异常处理

```python
try:
    print(obj.age)
except :
    print('error')  #--> error
finally :
    print(123)  # 不管有没有错都会执行
```
