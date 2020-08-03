---
title: 数据结构——广义表
date: 2020-01-24 09:13:15
tags:
- 算法
- 学习
categories:
- 数据结构
mathjax: true
description: 广义表（也称为列表）是$n(n\ge0)$个元素的有限序列。
---

### 广义表的定义

广义表（也称为列表）是$n(n\ge0)$个元素的有限序列。

记作：$LS=(a_1,a_2,...,a_3)$

其中：$LS$广义表名  $n$ $LS$的长度

$a_i(1\le i\le n)$或者是数据元素，或者是广义表。

通常，用大写字母表示广义表的名称，小写字母表示数据元素。当广义表$LS$中的元素是一个数据元素时，称其为原子，否则称为广义表的子表。

当广义表非空时，称第一个元素$a_1$为$LS$的表头(head)，称其余部分$(a_1,...,a_n)$为$LS$的表尾(tail)。

#### 广义表举例

1. $A=()$ A是一个空表，长度$n=0$。
2. $B=(e)$
   
   $Head(B)=e$  $Tail(B)=()$

3. $C=(a,(b,c))$

    $Head(C)=a$  $Tail(C)=((b,c))$

4. $D=((a,b),c)$

    $Head(D)=(a,b)$ $Tail(D)=(c)$

5. $E=((a,b),c,(d,e))$

    $Head(E)=(a,b)$ $Tail(E)=(c,(d,e))$

    $Head(Tail(E))=(c)$ $Tail(Tail(E))=((d,e))$

结论1：广义表允许共享子表。

结论2：广义表也允许递归的定义。

### 广义表的存储结构

由于广义表中的元素既可以是原子，也可以是广义表，所以会有原子结点和列表结点。

每个元素所需的空间大小无法统一，所以很难用顺序存储结构表示，通常采用链式结构表示。

原子结点：

![原子结点.png](data-structure7/原子结点.png)

只有两个域，标志域与值域。

列表结点：

![列表结点.png](data-structure7/列表结点.png)

有3个域，标志域，表头指针域与表尾指针域。

这种链式存储结构中，为了统一管理这2类结点，采用共用体（联合）来定义广义表的结点类型。

``` C++
typedef struct GLNode
{
    ElemTag tag; //标志域，用以区分原子结点和表结点
    union
    {
        AtomType atom; //原子结点
        struct
        {
            struct GLNode *hp,*tp;
        }ptr; //表结点
    }
}*GList;
```

### 广义表的递归算法

#### 求广义表的长度 `int GListLength(GList L)`

$$
递归定义为\begin{cases}
    0, \text{L==NULL}\\
    1+GListLength(L->ptr.tp), \text{L!=NULL}
\end{cases}
$$

``` C++
int GListlength(GList L)
{
    if(!L)
        return 0;
    return 1+GListLength(L->ptr.tp);
}
```

#### 求广义表的深度 `int GListDepth(GList L)`

广义表：$LS=(a_1,a_2,...,a_n)$

$$
递归定义为\begin{cases}
    1, \text{L==NULL(空表)}\\
    0, \text{L->tag==0(原子结点)}\\
    1+Max(a_i), \text{L!=NULL(非空表)}\\
\end{cases}
$$

``` C++
int GListDepth(GList L)
{
    if(!L)
        return 1;
    if(L->tag==0)
        return 0;
    for(max=0,p=L;p;p=p->ptr.tp)
    {
        dep=GListDepth(p->ptr.hp);
        if(dep>max)
            max=dep;
    }
    return max+1;
}
```