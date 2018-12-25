---
layout: post
title:  "Polynomial Multiplication"
date:   2018-12-26 00:42:36 +0330
categories: jekyll update
---
Polynomial Multiplication
<br>
$(a_{n}x^{n}+a_{n-1}x^{n-1}+...+a_{0}) \times (b_{m}x^{m}+b_{m-1}x^{m-1}+...+b_{0})=?$


```python
from IPython.display import display, Math, Latex
```


```python
def get_Polynomial():
    coefficients=[]
    powers=[]
    ch=True
    while ch:
        c_i=float(input("Enter i_th coefficient :"))
        coefficients.append(c_i)
        p_i=float(input("Enter n_th power :"))
        powers.append(p_i)
        check=str(input("Do you want to continue? (n=No/any other key=yes):"))
        if check=='n':
            ch=False
    return [coefficients,powers]
```


```python
def formal_f(x):
    if int(x)==x:
        x=int(x)
    return x
```


```python
def print_Polynomial(co_po):
    result=""
    for i in range(len(co_po[0])):
        if abs(co_po[0][i])!=1:
            if co_po[1][i]>1:
                result=result+'{}x^{}'.format(formal_f(co_po[0][i]),formal_f(co_po[1][i]))
            elif co_po[1][i]==1:
                result=result+'{}x'.format(formal_f(co_po[0][i]))
            else:
                result=result+'{}'.format(formal_f(co_po[0][i]))
        else:
            if co_po[0][i]>0:
                if co_po[1][i]>1:
                    result=result+'x^{}'.format(formal_f(co_po[1][i]))
                elif co_po[1][i]==1:
                    result=result+'x'
                else:
                    result=result+'{}'.format(formal_f(co_po[0][i]))
            else:
                if co_po[1][i]>1:
                    result=result+'-x^{}'.format(formal_f(co_po[1][i]))
                elif co_po[1][i]==1:
                    result=result+'-x'
                else:
                    result=result+'{}'.format(formal_f(co_po[0][i]))
        if i<len(co_po[0])-1:
            if co_po[0][i+1]>0:
                result=result+"+"
    return result
```


```python
def show_Formal(allE):
    display(Math(allE))
```


```python
def Polynomial_M(a,b):
    nc=[]
    np=[]
    for i in range(len(a[0])):
        for j in range(len(b[0])):
            nc.append(a[0][i]*b[0][j])
            np.append(a[1][i]+b[1][j])
    return [nc,np]
```


```python
def simplify_P(a):
    poly=a
    l=len(poly[0])
    i=0
    while i<l:
        j=i+1
        while j<l:
            if poly[1][i]==poly[1][j]:
                poly[0][i]+=poly[0][j]
                poly[0].pop(j)
                poly[1].pop(j)
                l-=1
                j-=1
            j+=1
        i+=1
    return poly
```


```python
def delet_z(a):
    poly=a
    l=len(poly[0])
    i=0
    while i<l:
        if a[0][i]==0:
            a[0].pop(i)
            a[1].pop(i)
            i-=1
            l-=1
        i+=1
    return poly
```


```python
def sort_P(poly):
    c_p=[]
    p_p=[]
    l=len(poly[0])
    for i in range(l):
        x=poly[0][0]
        y=poly[1][0]
        index=0
        for j in range(len(poly[0])):
            if y<poly[1][j]:
                x=poly[0][j]
                y=poly[1][j]
                index=j
        c_p.append(x)
        p_p.append(y)
        poly[0].pop(index)
        poly[1].pop(index)
    return [c_p,p_p]
```


```python
def full_simplify(poly):
    new=delet_z(poly)
    newp=simplify_P(new)
    newpp=delet_z(newp)
    return sort_P(newpp)
```


```python
def mp(a,b):
    na=full_simplify(a)
    nb=full_simplify(b)
    show_Formal("("+print_Polynomial(na)+")"+" \\times "+"("+print_Polynomial(nb)+")")
    resultP=Polynomial_M(na,nb)
    result=full_simplify(resultP)
    show_Formal("="+print_Polynomial(result))
    return result
```


```python
a=[[3, 4,], [2, 1]]
b=[[2,-5, 1], [3.0, 1,0]]
```


```python
ans=mp(a,b)
```


$$(3x^2+4x) \times (2x^3-5x+1)$$



$$=6x^5+8x^4-15x^3-17x^2+4x$$

