# 每日一句
Everything that has a beginning has an end.
世间万物有始皆有终。

# 概念

KMP 算法是一种改进的字符串匹配算法，由 D.E.Knuth、J.H.Morris和 V.R.Pratt 提出的，因此人们称它为克努特—莫里斯—普拉特算法（简称 KMP 算法）
KMP算法的核心是利用匹配失败后的信息，尽量减少模式串与主串的匹配次数以达到快速匹配的目的。具体就是通过一个 next() 函数来实现的，函数本身包含了模式串的局部匹配信息。
KMP 算法的时间复杂度O(m+n)

# 一个问题：有一个文本串S和一个模式串P，查找P在S中的位置，输出首次匹配的下标

下面思考这个问题应该怎么处理呢？


## 思路一：暴力匹配

假设现在文本串S匹配到 i 位置，模式串P匹配到 j 位置，则有：

- 如果当前字符匹配成功（S[i] == P[j]），则 i++，j++,继续匹配下一个字符

- 如果当前字符不匹配（S[i] ！= P[j]），则**令 i = i - （j-1）,j=0。 相当于每次匹配失败时，i 回溯，j被重置为 0.**

具体代码实现如下：

```C++
int ViolentMatch(char* s, char* p)
{
    int sLen = strlen(s);
    int pLen = strlen(p);
    int i = 0;
    int j = 0;
    while (i < sLen && j < pLen)
    {
        if (s[i] == p[j])
        {
            //①如果当前字符匹配成功（即S[i] == P[j]），则i++，j++    
            i++;
            j++;
        }
        else
        {
            //②如果失配（即S[i]! = P[j]），令i = i - (j - 1)，j = 0    
            i = i - j + 1;
            j = 0;
        }
    }
    //匹配成功，返回模式串p在文本串s中的位置，否则返回-1
    if (j == pLen)
        return i - j;
    else
        return -1;
}
```

## 思路二：KMP 算法


假设现在文本串S匹配到 i 位置，模式串P匹配到 j 位置

- 如果 j = -1，或者当前字符匹配成功（S[i] == P[j]），令j++，i++，继续匹配下一个字符


- 如果 j != -1，且当前字符匹配失败（S[i] != P[j]），则**令 i 不变，j = next[j]。**这里就是KMP与暴力匹配的区别，相较于暴力，KMP节约了找出下一个匹配点的时间



那么我们可以写出伪代码

```C++
int kmp(string s, string p) {
    int m = s.size(), n = p.size(), i = 0, j = 0;
    while (i < m && j < n) {
        if (j == - 1 || s[i] == p[j]) {
            ++i; ++j;
        } else {
            **j = next[j];**
        }
    }
    return (j == n) ? i - j : -1;
}
```

# 关于 next 数组你需要知道的

在前面我们已经知道了通过 next 数组可以利用匹配失败后的信息，尽量减少模式串与主串的匹配次数以达到快速匹配的目的。

那么它是怎么做到的呢？

我们先来了解下前置知识：最大前缀后缀公共元素

## 最大前缀后缀公共元素

这个概念指的是模式串中最大且相等的前缀和后缀。

下面举例说明

```text
# ABCDABD
"A"的前缀和后缀都为空集，共有元素的长度为0；
"AB"的前缀为[A]，后缀为[B]，共有元素的长度为0；
"ABC"的前缀为[A, AB]，后缀为[BC, C]，共有元素的长度0；
"ABCD"的前缀为[A, AB, ABC]，后缀为[BCD, CD, D]，共有元素的长度为0；
"ABCDA"的前缀为[A, AB, ABC, ABCD]，后缀为[BCDA, CDA, DA, A]，共有元素为"A"，长度为1；
"ABCDAB"的前缀为[A, AB, ABC, ABCD, ABCDA]，后缀为[BCDAB, CDAB, DAB, AB, B]，共有元素为"AB"，长度为2；
"ABCDABD"的前缀为[A, AB, ABC, ABCD, ABCDA, ABCDAB]，后缀为[BCDABD, CDABD, DABD, ABD, BD, D]，共有元素的长度为0。

对应关系：
ABCDABD
0000120
```

利用最大前缀后缀公共元素，我们可以知道：**第一次的最大后缀就是下一次的最大前缀**。一定要好好理解这句话，下面举例说明

第一次：
文本串S：BBC ABCDAB**C**ABCDABCDABDE
模式串P：         ABCDAB**D**

可以看到在上面的加粗部分 C ≠D 失配，对于失配处"ABCDAB"，它的最大公共前后缀元素为"AB"，长度为2，根据**第一次的最大后缀就是下一次的最大前缀**，那么就有：
下一次：

文本串S：BBC ABCDAB**C**ABCDABCDABDE
模式串P：                    AB**C**DABD

而如果是暴力算法的话，这应该是这样的：

文本串S：BBC A**B**CDABCABCDABCDABDE
模式串P：            **A**BCDABD

可以看到使用这种思想，可以减少模式串与主串的匹配次数。

## 计算next数组

我们现在已经知道了可以通过最大长度来快速匹配，那么怎么求出最大长度呢？

待续...






# 美文佳句

其实，一场适逢的黄昏雨，更是醉秋不可或缺的滋润剂。风一定是徐徐而过，斜斜地，擦拭过你的眉毛，像亲人的呼唤，又有满怀期许的温暖，雨不急，裹挟着些许凉意，但并不寒凉，和着风，从眼前飘过，飘成丝丝缕缕的锦绸，从山巅飘向阔野，像往事的一些片段，走向记忆的深处。而黄昏的幕布，正迎着记忆走远的方向，围拢而来，低处村舍的灯火，也渐次明灭，透过窗棂，躲躲闪闪里，开始诉说秋之静夜。

此刻，唯有立于山野的你，还迷醉在秋之醇香里，像一枚叹号，亟待着谁人温热的双手，皈依秋天的诗句！ 