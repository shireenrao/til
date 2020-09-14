# Decorators

Here are some basics on decorators. The code below shows the following

1. Create a basic decorator
2. Make sure docstrings work
3. Allow functions you are decorating have arguments (*args, **kwargs)
4. Allow decorators to have arguments
5. Show how multiple decorators work
6. Class Based decorators

```python
>>> import time
>>> from functools import wraps
>>> def logger(func):
	"""Decorator to log functions"""
	def log():
		"""log function"""
		start = time.perf_counter()
		func()
		print(f"{func.__name__} took {time.perf_counter() - start:.5f} seconds")
	return log

>>> @logger
def compute():
	return sum(range(100000))

>>> compute()
compute took 0.00534 seconds
>>> 
>>> 
>>> compute.__doc__
'Logger function'
>>> def logger(func):
	"""Logger Decorator"""
	@wraps(func)
	def logit():
		"""Logger function"""
		start = time.perf_counter()
		func()
		print(f"{func.__name__} took {time.perf_counter() - start:.5f} seconds")
	return logit

>>> @logger
def compute():
	"""Computer function"""
	return sum(range(1000000))

>>> compute()
compute took 0.05905 seconds
>>> compute.__doc__
'Computer function'
>>> @logger
def compute(n):
	"""Computer function"""
	return sum(range(n))

>>> compute(10000)
Traceback (most recent call last):
  File "<pyshell#50>", line 1, in <module>
    compute(10000)
TypeError: logit() takes 0 positional arguments but 1 was given
>>> def logger(func):
	"""Logger Decorator"""
	@wraps(func)
	def logit(n):
		"""Logger function"""
		start = time.perf_counter()
		func(n)
		print(f"{func.__name__} took {time.perf_counter() - start:.5f} seconds")
	return logit

>>> @logger
def compute(n):
	"""Computer function"""
	return sum(range(n))

>>> compute(10000)
compute took 0.00041 seconds
>>> compute(1000000)
compute took 0.05945 seconds

>>> def logger(unit):
	"""Logger Decorator"""
	def logit(func):
		"""Logger function"""
		@wraps(func)
		def logit_inner(n):
			start = time.perf_counter()
			func(n)
			state = 1000 if unit == "ms" else 1
			print(f"{func.__name__} took {(time.perf_counter() - start) * state:.5f} {unit}")
		return logit_inner
	return logit

>>> @logger("ms")
def compute_ms(n):
	"""Computer function"""
	return sum(range(n))

>>> @logger("s")
def compute_s(n):
	"""Computer function"""
	return sum(range(n))

>>> compute_ms(1000000)
compute_ms took 59.15670 ms
>>> compute_s(1000000)
compute_s took 0.05758 s
>>> compute_ms.__doc__
'Computer function'
>>> compute_s.__doc__
'Computer function'
>>> def repeater(num):
	"""Decorator to repeat num times"""
	def repeat(func):
		"""Repeat function"""
		@wraps(func)
		def inner_repeat(*args, **kwargs):
			for _ in range(num):
				func(*args, **kwargs)
		return inner_repeat
	return repeat

>>> @repeater(2)
def say_hi(name):
	print(f"Hi {name}")

	
>>> say_hi("John")
Hi John
Hi John
>>> @repeater(2)
@logger("ms")
def compute(n):
	"""Computer function"""
	return sum(range(n))

>>> compute(500000)
compute took 39.08660 ms
compute took 54.54620 ms
>>> @repeater(2)
@logger("ms")
def say_hi(name):
	print(f"Hi {name}")

	
>>> say_hi("John")
Hi John
say_hi took 22.75060 ms
Hi John
say_hi took 23.97130 ms
>>> @logger("ms")
@repeater(2)
def say_hi(name):
	print(f"Hi {name}")

	
>>> say_hi("John")
Hi John
Hi John
say_hi took 58.48050 ms
>>> class Repeater:
	def __init__(self, n):
		self.n = n
	def __call__(self, func):
		def repeater(*args, **kwargs):
			for _ in range(self.n):
				func(*args, **kwargs)
		return repeater

	
>>> @Repeater(n=2)
def say_hello(person):
	print(f"Hello {person}")

>>> say_hello("Jim")
Hello Jim
Hello Jim
>>> 
```

