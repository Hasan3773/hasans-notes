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

``` Python
class Solution(object):
    def topKFrequent(self, nums, k):
        map = {}
        for i, n in enumerate(nums):
            if n not in map:
                map[n] = 1
            else:
                map[n] += 1
        sorted_map = sorted(map.items(), key=lambda x:x[1], reverse=True)
        print(sorted_map)
        result = [0] * k
        j = 0
        while(j < k):
            result[j] = sorted_map[j][0]
            print(j)
            j += 1
        return result
```















Incorrect: 
```Python
       sorted_nums = sorted(nums)
        print(sorted_nums)
        answer = []
        for i, n in enumerate(sorted_nums):
            if i+1 == len(nums):
                if n - 1 == sorted_nums[i - 1]:
                    print("first", n)
                    if n not in answer:
                        answer.append(n)
            elif n + 1 == sorted_nums[i+1] and n - 1 == sorted_nums[i-1]:
                print("second", n)
                if n not in answer:
                    answer.append(n)
                    if n + 1 == sorted_nums[i+1]:
                        answer.append(n+1)
                    elif n - 1 == sorted_nums[i-1]:
                        answer.append(n-1)
        print(answer, len(nums))
        if not answer and len(nums) != 0:
            return 1
        return len(answer)
```

```Python 
	def longestConsecutive(self, nums):
       max_count = 0
        for num in nums:
            current_num = num
            current_count = 1
            while(current_num + 1 in nums):
                current_count += 1
                current_num += 1
            max_count = max(current_count, max_count)
        return max_count
```
