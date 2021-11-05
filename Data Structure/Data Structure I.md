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

### 1. Two Sum

Given an array of integers *nums* and an integer *target*, return indices of the two numbers such that they add up to *target*.

You may assume that each input would have *exactly one solution*, and you may not use the same element twice.

You can return the answer in any order.

Example 1:

Input: nums = [2,7,11,15], target = 9

Output: [0,1]

Output: Because nums[0] + nums[1] == 9, we return [0, 1].

Example 2:

Input: nums = [3,2,4], target = 6

Output: [1,2]

Example 3:

Input: nums = [3,3], target = 6

Output: [0,1]

Constraints:

* 2 <= nums.length <= 10^4
* -10^9 <= nums[i] <= 10^9
* -10^9 <= target <= 10^9
* Only one valid answer exists.

Follow-up: Can you come up with an algorithm that is less than O(n2) time complexity?

#### Answer 3

```javascript
var twoSum = function(nums, target) {
    // Define a hashmap to store values, indices
    const map = new Map();
    
    for (let i = 0; i < nums.length; i++) {
        // Define current number, current diff
        const num = nums[i];
        const diff = target - num;
                
        // If hashmap contains difference, return stored index and current index
        if (map.has(diff)) return [map.get(diff), i];
        
        // Store (key: value => number: index) in hashmap
        map.set(num, i);
    }
};

//Your input
[2,7,11,15]
9
//Output
[0,1]
//Expected
[0,1]
```

### 88. Merge Sorted Array

You are given two integer arrays *nums1* and *nums2*, sorted in *non-decreasing order*, and two integers *m* and *n*, representing the number of elements in *nums1* and *nums2* respectively.

*Merge nums1 and nums2* into a single array sorted in *non-decreasing order*.

The final sorted array should not be returned by the function, but instead be stored inside the array *nums1*. To accommodate this, *nums1* has a length of *m + n*, where the first *m* elements denote the elements that should be merged, and the last *n* elements are set to *0* and should be ignored. *nums2* has a length of *n*.

Example 1:

Input: nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3

Output: [1,2,2,3,5,6]

Explanation: The arrays we are merging are [1,2,3] and [2,5,6].
The result of the merge is [1,2,2,3,5,6] with the underlined elements coming from nums1.

Example 2:

Input: nums1 = [1], m = 1, nums2 = [], n = 0

Output: [1]

Explanation: The arrays we are merging are [1] and [].
The result of the merge is [1].

Example 3:

Input: nums1 = [0], m = 0, nums2 = [1], n = 1

Output: [1]

Explanation: The arrays we are merging are [] and [1].
The result of the merge is [1].
Note that because m = 0, there are no elements in nums1. The 0 is only there to ensure the merge result can fit in nums1.

Constraints:

* nums1.length == m + n
* nums2.length == n
* 0 <= m, n <= 200
* 1 <= m + n <= 200
* -10^9 <= nums1[i], nums2[j] <= 10^9

Follow up: Can you come up with an algorithm that runs in *O(m + n)* time?

#### Answer 4

```javascript
var merge = function (nums1, m, nums2, n) {
    nums1.splice(m); // removes all 0's
    for (var i = 0; i < n; i++) {
        nums1.unshift(nums2[i]); // inserts each number from nums2 to the beggining of nums1
    }
    nums1.sort((a, b) => a - b); // sorts the array
};

//Your input
[1,2,3,0,0,0]
3
[2,5,6]
3
//Output
[1,2,2,3,5,6]
//Expected
[1,2,2,3,5,6]
```

### 350. Intersection of Two Arrays II

Given two integer arrays *nums1* and *nums2*, return an array of their intersection. Each element in the result must appear as many times as it shows in both arrays and you may return the result in *any order*.

Example 1:

Input: nums1 = [1,2,2,1], nums2 = [2,2]

Output: [2,2]

Example 2:

Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]

Output: [4,9]

Explanation: [9,4] is also accepted.

Constraints:

* 1 <= nums1.length, nums2.length <= 1000
* 0 <= nums1[i], nums2[i] <= 1000

Follow up:

* What if the given array is already sorted? How would you optimize your algorithm?
* What if nums1's size is small compared to nums2's size? Which algorithm is better?
* What if elements of nums2 are stored on disk, and the memory is limited such that you cannot load all elements into the memory at once?

#### Answer 5

```javascript
var intersect = function(nums1, nums2) {
  const res = [], n1 = {}, n2 = {};
  for (let i = 0; i < Math.max(nums1.length, nums2.length); i++) {
    let num1 = nums1[i], num2 = nums2[i];
    n1[num1] = n1[num1] + 1 || 1, n2[num2] = n2[num2] + 1 || 1;
    [num1, num2].forEach(num => {
      if (n1[num] && n2[num]) {
        n1[num]--, n2[num]--;
        res.push(num);
      }
    })
  }
  return res;
};

var intersect = function(nums1, nums2) {
    // sort the arrays
    nums1.sort((a,b) => a-b), nums2.sort((a,b) => a-b);

    let i = 0,
        j = 0,
        result = [];
    
    while(i<nums1.length && j<nums2.length) {
        if(nums1[i] < nums2[j]){
            i++;
        } else if(nums1[i] > nums2[j]) {
            j++;
        } else {
            result.push(nums1[i]);
            i++;
            j++;
        }
    }
    
    return result;
};

//Your input
[1,2,2,1]
[2,2]
//Output
[2,2]
//Expected
[2,2]
```

### 121. Best Time to Buy and Sell Stock

You are given an array prices where prices[i] is the price of a given stock on the ith day.

You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.

Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.

Example 1:

Input: prices = [7,1,5,3,6,4]

Output: 5

Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.

Example 2:

Input: prices = [7,6,4,3,1]

Output: 0

Explanation: In this case, no transactions are done and the max profit = 0.

Constraints:

* 1 <= prices.length <= 10^5
* 0 <= prices[i] <= 10^4

#### Answer 6

```javascript
var intersect = function(nums1, nums2) {
  const res = [], n1 = {}, n2 = {};
  for (let i = 0; i < Math.max(nums1.length, nums2.length); i++) {
    let num1 = nums1[i], num2 = nums2[i];
    n1[num1] = n1[num1] + 1 || 1, n2[num2] = n2[num2] + 1 || 1;
    [num1, num2].forEach(num => {
      if (n1[num] && n2[num]) {
        n1[num]--, n2[num]--;
        res.push(num);
      }
    })
  }
  return res;
};

var intersect = function(nums1, nums2) {
    // sort the arrays
    nums1.sort((a,b) => a-b), nums2.sort((a,b) => a-b);

    let i = 0,
        j = 0,
        result = [];
    
    while(i<nums1.length && j<nums2.length) {
        if(nums1[i] < nums2[j]){
            i++;
        } else if(nums1[i] > nums2[j]) {
            j++;
        } else {
            result.push(nums1[i]);
            i++;
            j++;
        }
    }
    
    return result;
};

//Your input
[1,2,2,1]
[2,2]
//Output
[2,2]
//Expected
[2,2]
```
