# Interesting Tips

Saw this tip which frameworks like Django might be use for dynamic attribute setting based on list of fields


```python
>>> class Structure:
	_fields = []
	def __init__(self, *args):
		for name, val in zip(self._fields, args):
			setattr(self, name, val)

			
>>> class Stock(Structure):
	_fields = ["name", "shares", "price"]

	
>>> class Point(Structure):
	_fields = ["x", "y"]

	
>>> class Address(Structure):
	_fields = ["hostname", "port"]

	
>>> s = Stock("Google", 100, 200)
>>> vars(s)
{'name': 'Google', 'shares': 100, 'price': 200}
>>> p = Point(4, 6)
>>> vars(p)
{'x': 4, 'y': 6}
>>> a = Address("localhost", 9000)
>>> vars(a)
{'hostname': 'localhost', 'port': 9000}
```
