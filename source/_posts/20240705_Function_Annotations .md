---
title: Function Annotations
date: 2024-07-05 08:12:55
tags:
  - python
categories:
  - python
---

## Understanding Function Annotations `->` ，`:`

Today I would like to share when we see an arrow or colon on function, basically there's a term `Function Annotation`. I see some turtorial and see many developer beeen using it, and went and research on it.

You can think it's just a comment, nothing else. It to tell people about your code expectation, like data type or return value. So let me show you some examples, and you will see the arrow or colon doesn't mean anything, it just to tell people what this variable mean.

```
def velocity(s: 'in miles', t: 'in hours') ->'mph':
    return s/t

velocity(4,5) # 0.8

print(velocity.__annotations__)
```

> output:
>
> > `{'s': 'in miles', 't': 'in hours', 'return': 'mph'}`

from above example it just to tell user `s` is in mile, `t` is in hours, and return mph

You will see many people use like this to define datatype:

```
def calculate(a: int, b: int)-> int:
    return a+b
result= calculate(4,5)
print(calculate.__annotations__)
# {'a': <class 'int'>, 'b': <class 'int'>, 'return': <class 'int'>}
```

overall it just to tell people what the code expectation is or are.
