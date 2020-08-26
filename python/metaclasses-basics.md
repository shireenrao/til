# MetaClasses Basics

Here is a snippet to show how you can control Class construction. This snippet is from David Beazley Tutorial

```python
class mytype(type):
    def __new__(cls, clsname, bases, clsdict):
        if len(bases) > 1:
            raise TypeError("No!!")
        return super().__new__(cls, clsname, bases, clsdict)


class Base(metaclass=mytype):
    pass


class A(Base):
    pass


class B(Base):
    pass


class C(A, B):
    pass

Traceback (most recent call last):
  File "<pyshell#19>", line 1, in <module>
    class C(A, B):
  File "<pyshell#5>", line 4, in __new__
    raise TypeError("No!!")
TypeError: No!!
```

