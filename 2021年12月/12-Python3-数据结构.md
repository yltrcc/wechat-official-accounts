# 每日一句
I just have to live my truth.
我必须活出真实的自己。

在本章节中我们将会学到 Python 中的数据结构。

# 列表

Python中列表是可变的，这是它区别于字符串和元组的最重要的特点，一句话概括即：列表可以修改，而字符串和元组不能。

|||
|-|-|
|方法|描述<br>|
|list.append(x)|把一个元素添加到列表的结尾，相当于 a[len(a):] = [x]。|
|list.extend(L)|通过添加指定列表的所有元素来扩充列表，相当于 a[len(a):] = L。|
|list.insert(i, x)|在指定位置插入一个元素。第一个参数是准备插入到其前面的那个元素的索引，例如 a.insert(0, x) 会插入到整个列表之前，而 a.insert(len(a), x) 相当于 a.append(x) 。|
|list.remove(x)|删除列表中值为 x 的第一个元素。如果没有这样的元素，就会返回一个错误。|
|list.pop([i])|从列表的指定位置移除元素，并将其返回。如果没有指定索引，a.pop()返回最后一个元素。元素随即从列表中被移除。（方法中 i 两边的方括号表示这个参数是可选的，而不是要求你输入一对方括号，你会经常在 Python 库参考手册中遇到这样的标记。）|
|list.clear()|移除列表中的所有项，等于del a[:]。|
|list.index(x)|返回列表中第一个值为 x 的元素的索引。如果没有匹配的元素就会返回一个错误。|
|list.count(x)|返回 x 在列表中出现的次数。|
|list.sort()|对列表中的元素进行排序。|
|list.reverse()|倒排列表中的元素。|
|list.copy()|返回列表的浅复制，等于a[:]。|


下面示例演示了列表的大部分方法：

```text

a = [66.25, 333, 333, 1, 1234.5]
print(a.count(333), a.count(66.25), a.count('x'))
a.insert(2, -1)
print(a)
a.append(333)
print(a)
print(a.index(333))
a.remove(333)
print(a)
a.reverse()
print(a)
a.sort()
print(a)

执行结果：
210
[66.25, 333, -1, 333, 1, 1234.5]
[66.25, 333, -1, 333, 1, 1234.5, 333]
1
[66.25, -1, 333, 1, 1234.5, 333]
[333, 1234.5, 1, 333, -1, 66.25]
[-1, 1, 66.25, 333, 333, 1234.5]

```

**注意：类似 insert, remove 或 sort 等修改列表的方法没有返回值。**

# 美文佳句

凡事说着容易，做着难。人在气头上，就像洪水翻滚，要立马停下来并退让，那是需要极大的自控力、极宽的胸襟与极高的修养的。

孔子也曾教“得理”的颜回“让人”。

买布的与卖布的起了纠纷，买布的嚷：“三八就是二十三，为啥要我二十四个钱？”颜回路过，就插嘴其中，欲摆平此事，结果引火烧身，买布的赌上了“头”，颜回赌上了“冠”。找孔子评判，孔子判颜回输。

让了，颜回只是输了“冠”；不让，那就是一个脑袋。得理也让人，孔子教颜回赢的是人格。

这有意义的一堂生活课，上了二千余年，一直到今天仍散发着光辉。

可见“得理”，仍需让三分。不妨一试，海阔天空。