## Recursion

```python
def binary_search(data, target, low, high):
	if low > high:
		return False
	else:
		mid = (low+high)//2
		if data[mid] == target:
			return True
		elif data[mid] > target:
			return binary_search(data, target, low, mid-1)
		elif data[mid] < target:
			return binary_search(data, target, mid+1, high)


a = [3,5,7,9,15,20]
target = 7
print(binary_search(a, target, 0, len(a)-1))

def binary_iter_search(data, target, low, high):
	while(low <= high):
		mid = (low+high)//2
		if data[mid] == target:
			return True
		elif target < data[mid]:
			high = mid-1
		elif target > data[mid]:
			low = mid+1
	return False

a = [3,5,9,15,20]
target = 7
print(binary_iter_search(a, target, 0, len(a)-1))
```
