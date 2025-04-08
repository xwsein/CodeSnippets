### Problem Overview

The “Two Sum” problem is one of those classic challenges you’ll often find on coding platforms like LeetCode, and it’s a great place to start if you’re preparing for coding interviews. Here’s the gist of it:

You’re given an array of integers, `nums`, and a target integer, `target`. Your task is to find two distinct numbers in the array that add up to the target, and return their indices.

---

### Problem Example

Let’s look at an example to make things clearer:

**Input:**
```python
nums = [2, 7, 11, 15]
target = 9
```

**Output:**
```python
[0, 1]
```

**Explanation:**  
Because `nums[0] + nums[1] == 9`, we return `[0, 1]`.  
Here, we have the numbers `2` and `7`, which together add up to `9`, so we return their indices: `[0, 1]`.

---

### How to Approach It?

There are several ways to approach this problem, but let’s go over the three main ones: Brute Force, Using a Hash Map, and Two Pointers.

---

#### 1. Brute Force Approach (The Naive Way)

This is the first solution that might come to mind, but it’s not the most efficient. The idea is simple: you check every possible pair of numbers to see if they add up to the target.

**Steps:**
1. Use two loops to go through each number in the array.
2. For each number, check if adding it to any of the numbers after it results in the target.
3. If you find a match, return the indices.

**Time Complexity:** `O(n²)` — You have two loops going through the array, which isn’t great for performance with larger lists.

**Code Example:**
```python
def twoSum(nums, target):
    for i in range(len(nums)):
        for j in range(i + 1, len(nums)):
            if nums[i] + nums[j] == target:
                return [i, j]
```

---

#### 2. Using a Hash Map (The Smart Way)

A more efficient solution involves using a hash map (also known as a dictionary in Python). The idea is to remember the numbers you’ve seen so far as you go through the list and check if the complement (the number that, when added to the current number, equals the target) is already in the hash map.

**Steps:**
1. Traverse the array while keeping track of the indices of the numbers you’ve seen in a dictionary.
2. For each number, calculate the complement (`target - current_number`) and check if it’s already in the dictionary.
3. If you find the complement, return the indices of the two numbers.

**Time Complexity:** `O(n)` — You only need to go through the array once, and dictionary lookups are fast.

**Code Example:**
```python
def twoSum(nums, target):
    num_map = {}
    for i, num in enumerate(nums):
        complement = target - num
        if complement in num_map:
            return [num_map[complement], i]
        num_map[num] = i
```

This solution is much more efficient than the brute force one.

---

#### 3. Using Sorting + Two Pointers (An Alternative)

This approach works by first sorting the array, then using two pointers to find two numbers that add up to the target.

**Steps:**
1. First, sort the array while keeping track of the original indices.
2. Then, use two pointers: one starts at the beginning, and the other starts at the end.
3. Move the pointers towards each other based on the sum of the numbers at those positions.
4. If the sum is less than the target, move the left pointer to the right.
5. If the sum is greater than the target, move the right pointer to the left.

**Time Complexity:** `O(n log n)` — Sorting takes `O(n log n)`, and the two-pointer pass takes `O(n)`.

**Code Example:**
```python
def twoSum(self, nums, target):
    nums_sorted = sorted([(num, i) for i, num in enumerate(nums)], key=lambda x: x[0])
    left, right = 0, len(nums) - 1
    
    while left < right:
        current_sum = nums_sorted[left][0] + nums_sorted[right][0]
        if current_sum == target:
            return [nums_sorted[left][1], nums_sorted[right][1]]
        elif current_sum < target:
            left += 1
        else:
            right -= 1
```

This approach requires sorting the array, which isn’t as efficient as the hash map solution but is still better than brute force.

---

### Which Approach Is Best?

Let’s compare the three methods:

| Approach               | Time Complexity | Space Complexity | Explanation |
|------------------------|-----------------|------------------|-------------|
| **Brute Force**         | `O(n²)`         | `O(1)`           | Simple but inefficient for larger arrays. |
| **Hash Map**            | `O(n)`          | `O(n)`           | Optimal in terms of time and space. |
| **Sorting + Two Pointers** | `O(n log n)`   | `O(n)`           | Good if you’re okay with sorting, but not as fast as the hash map solution. |

**Conclusion:**  
The **Hash Map** approach is generally the best in terms of performance for this problem, with `O(n)` time complexity and `O(n)` space complexity.

---

### Wrapping Up

The Two Sum problem is a great exercise for learning how to think about time complexity and data structures like hash maps. The problem teaches you how to solve it in multiple ways, giving you practice with common interview techniques.

It’s also a good example of how sometimes extra space (like a hash map) can save you time in the long run. So if you’re preparing for coding interviews, mastering this problem will give you a solid understanding of hash maps and how they can be used to optimize solutions.

---
