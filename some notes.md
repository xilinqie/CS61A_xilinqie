---
data: 2025-08-18
tags:
  - Python
  - CS
  - Learn
---
# Lec2

1. 赋值语句
```python
a = 10
b = 20
a , b = a + b , a
```

这不是一个逗号表达式，而是两个赋值语句，而且这两个赋值语句是在同时进行的，不存在先后。
	同时进行：输出结果：a = 30；b = 10（✅）
	先后进行：输出结果：a = 30；b = 30（❌）

2. 函数返回值问题：
当一个函数没有返回值的时候，他返回的就是None（None value is not displayed），
解释器不会将None显示为表达式的值 

3. Pure Function vs Non- Pure Function  



# Lec3
1. 运算符工作原理：
	- +：add
	- \*：mul
	- /：精确的除法
	- //：整数除法
```python
from operator import add, mul
from operator import truediv, floordiv
from operator import mod

def divide_exact(n,d):
	return n//d,n%d

quotient, reminder = divide_exact(2013,10)
//quotient = 201
//reminder = 3
```

2. 学会在def自定义函数的下一行就对函数进行注释
3. python中的自定义函数也可以进行重载、自定义默认参数
```python
def devide_exact(n, d=10)
```
4. if语句：
```python
def absolute_value(x):
	if x < 0:
		return -x
	elif x==0:
		return 0
	'''
	这中间还可以加上很多个elif语句
	'''
	else:
		return x
```
5. python中的True和False
False value：False；0；''；None
True value：anything else


# Lec4
1. 逻辑运算符的短路
```python
False and Anythin => False
True or Anything => True
```
应用举例：
```python
def has_big_sqrt (n):
	return n > 0 and sqrt(n) > 10
```

2. assert断言
```python
assert r>0, 'A Length must bigger than 0'
assert 2<1, ' See what happened'
```
```bash
(base) ericw@Erics-MBA Python_CS61A % /usr/local/bin/python3 /Users/ericw/Desktop/二年级上/自学/Python_CS61A/Lec1/lec1.py
Traceback (most recent call last):
  File "/Users/ericw/Desktop/二年级上/自学/Python_CS61A/Lec1/lec1.py", line 72, in <module>
    assert 2<1, ' See what happened'
           ^^^
AssertionError:  See what happened
```

3. 函数嵌套函数，然后返回值还是函数
```python
def add_two(n):
	def add_two_helper(k):
		return k+n
	return add_two_helper
	
print(add_two(2)(3))
'''
>>> add_two(3)(4)
>>> 7
'''
```


# Lec5
1. 函数可以作为参数传入一个函数，也需要在定义后者函数的时候就写出参数是函数。
```python
def apply_twice (f,x):
	return f(f(x))
def square(x):
	return x*x

>>> python -i lec1.py
>>> apply_twice(square,4)
>>> 256
```

2. 函数的嵌套，注意作用域的范围限制
```python
def make_adder(n):
	def adder(x):
		return n+x
	return adder
	
print(make_adder(5)(10)) # Should print 15
add_five = make_adder(5)
print(add_five(10))
```

3. $lambda$表达式，与$def$函数的区别就是，没有办法使用语句，只能使用表达式
```python
square = lambda x: x*x
print(square(5))
print((lambda x: x*x)(5))
```

4. 单参数函数的多层嵌套与函数的$curry$化
```python
from operator import add
def curry2(f):
	def g(x):
		def h(y):
			return f(x,y)
		return h
	return g
print(curry2(add)(3)(2))
print((lambda f: lambda x: lambda y: f(x, y))(add)(3)(2))
```

