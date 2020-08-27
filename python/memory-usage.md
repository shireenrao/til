# Memory Usage

How to tell how much memory is being used for a given datastructure. 
You would think one could use `sys.getsizeof`, but that does not give 
you the real amount of memory used. 

One reasonable way for platform independent use is:

```python
import tracemalloc
tracemalloc.start()
data = read_data("somebigfile")
print(tracemalloc.get_traced_memory())
```
