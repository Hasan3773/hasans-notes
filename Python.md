```Python
def twoSum(self, nums, target):
	map = {}
	for i, n in enumerate(nums):
		if target - n in map:
			return [i, map[target - n]]
		else:
			map[n] = i
```

``` Python
def isPalindrome(self, s):
	cleanstring = ''.join(c.lower() for c in s if(c.isalnum()))
	one = 0 
	two = len(cleanstring) - 1

	while (one < two):
		if (cleanstring[one] != cleanstring[two]):
			return False
		one += 1
		two -= 1

	return True 
```

```Python
@pytest.mark.parametrize("sensor_val, min_val, max_val", [
    (25.0, 20.0, 30.0),
    (3.3, 3.0, 3.6),
    (-5.0, -10.0, 50.0)
])

def test_sensor_bounds(sensor_val, min_val, max_val):
    assert min_val <= sensor_val <= max_val, f"Value {sensor_val} out of bounds."
```
