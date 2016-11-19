range 和 xrange
===============
range([start,] stop[, step])，根据start与stop指定的范围以及step设定的步长，生成一个序列。xrange 用法与 range 完全相同，所不同的是生成的不是一个list对象，而是一个生成器。

```python
>>> range(5) 
[0, 1, 2, 3, 4] 
>>> range(1,5) 
[1, 2, 3, 4] 
>>> range(0,6,2)
[0, 2, 4]

>>> xrange(5)
xrange(5)
>>> list(xrange(5))
[0, 1, 2, 3, 4]
>>> xrange(1,5)
xrange(1, 5)
>>> list(xrange(1,5))
[1, 2, 3, 4]
>>> xrange(0,6,2)
xrange(0, 6, 2)
>>> list(xrange(0,6,2))
[0, 2, 4]
```

多重赋值
========
```python
>>> t = 1,2,3
>>> t
(1, 2, 3)
>>> a,b,c = t
>>> a
1
>>> b
2
>>> c
3
```
多重赋值本质就是 tuple packing （元组打包）和 Sequence unpacking（序列解包）。

```python
>>> t = a, b, c    
# 这就是tuple packing，按照tuple的构建的语法，我们知道这里t肯定是个tuple。
```
```python
>>> a, b, c = t
# 这就是Sequence unpacking，这里t只要是三元的Sequence就可以了，不一定是tuple，
# 如果t不是三元的，会抛出一个ValueError异常。
```

Python 的多重赋值是个很好用的语法糖，比如能让一行中完成一次交换：
```python
>>> a = 2
>>> b = 3
>>> a,b = b,a
>>> a
3
>>> b
2
``
