# Data Structure I

In computer science, a **data structure** is a way to store and organize data.

During the computer programming process, identifying and using the appropriate data structure is an important task as it can improve the overall efficiency of the *algorithm*. In large-scale systems, choosing the most suitable data structure directly impacts the difficulty of program design and the final quality and performance.

## Array

### 217. Contains Duplicate

Given an integer array *nums*, return *true* if any value appears *at least twice* in the array, and return *false* if every element is distinct.

Example 1:

Input: nums = [1,2,3,1]

Output: true

Example 2:

Input: nums = [1,2,3,4]

Output: false

Example 3:

Input: nums = [1,1,1,3,3,4,3,2,4,2]
Output: true

Constraints:

* 1 <= nums.length <= 10^5
* -10^9 <= nums[i] <= 10^9

#### Answer 1

```javascript
var containsDuplicate = n => new Set(n).size !== n.length;

//Your input
[1,2,3,1]
//Output
true
//Expected
true

// Alternate early return version:
function containsDuplicate(nums, set = new Set()) {
  for (let num of nums) {
    if (set.has(num)) return true;
    set.add(num);
  }
  return false;
};
```

### 53. Maximum Subarray

Given an integer array *nums*, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

A subarray is a contiguous part of an array.

Example 1:

Input: nums = [-2,1,-3,4,-1,2,1,-5,4]

Output: 6

Explanation: [4,-1,2,1] has the largest sum = 6.

Example 2:

Input: nums = [1]

Output: 1

Example 3:

Input: nums = [5,4,-1,7,8]

Output: 23

Constraints:

* 1 <= nums.length <= 10^5
* -10^4 <= nums[i] <= 10^4

#### Answer 2

```javascript
var maxSubArray = function(nums) {
    let [max] = nums, right = 0;
  while (right < nums.length) {
      nums[right] += nums[right-1] > 0 ? nums[right-1] : 0;
    
      max = Math.max(max, nums[right++]);
  }
  return max;
};

//Your input
[-2,1,-3,4,-1,2,1,-5,4]
//Output
6
//Expected
6
```
