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
#### Difference between return and print
Unfortunately, there is a character limit so this will be in many parts. First thing to note is that return and print are statements, not functions, but that is just semantics.

I'll start with a basic explanation. print just shows the human user a string representing what is going on inside the computer. The computer cannot make use of that printing. return is how a function gives back a value. This value is often unseen by the human user, but it can be used by the computer in further functions.

On a more expansive note, print will not in any way affect a function. It is simply there for the human user's benefit. It is very useful for understanding how a program works and can be used in debugging to check various values in a program without interrupting the program.

return is the main way that a function returns a value. All functions will return a value, and if there is no return statement (or yield but don't worry about that yet), it will return None. The value that is returned by a function can then be further used as an argument passed to another function, stored as a variable, or just printed for the benefit of the human user.

Consider these two programs:
```
def function_that_prints():
    print "I printed"

def function_that_returns():
    return "I returned"

f1 = function_that_prints()
f2 = function_that_returns()
print "Now let us see what the values of f1 and f2 are"
print f1
print f2
```
