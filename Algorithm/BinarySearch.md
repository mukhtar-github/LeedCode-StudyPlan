# Algorithm

## 704. Binary Search

Given an array of integers nums which is sorted in ascending order, and an integer target, write a function to search target in nums. If target exists, then return its index. Otherwise, return -1.

You must write an algorithm with O(log n) runtime complexity.

Example 1:

Input: nums = [-1,0,3,5,9,12], target = 9

Output: 4

Explanation: 9 exists in nums and its index is 4

Example 2:

Input: nums = [-1,0,3,5,9,12], target = 2

Output: -1

Explanation: 2 does not exist in nums so return -1

Constraints:

1 <= nums.length <= 10^4

-10^4 < nums[i], target < 10^4

All the integers in nums are unique. nums is sorted in ascending order

### Answer 1

```javascript
var search = function (nums, target) {
    let start = 0;
    let end = nums.length - 1;

    while (start <= end) {
        let mid = Math.round((start + end) / 2);
        if (nums[mid] === target) {
            return mid;
        } else if (nums[mid] < target) {
            start = mid + 1;
        } else {
            end = mid - 1;
        }
    }
    return -1;
};

// Your input => [-1,0,3,5,9,12]
// 9
// Output => 4
// Expected => 4
```

### Approach 1: Binary Search

#### Intuition

Binary search is a textbook algorithm based on the idea to compare the target value to the middle element of the array. If the target value is equal to the middle element - we're done. If the target value is smaller - continue to search on the left. If the target value is larger - continue to search on the right.

#### Algorithm 1

* Initialise left and right pointers : left = 0, right = n - 1.

* While left <= right :

* Compare middle element of the array nums[pivot] to the target value target.

* If the middle element is the target target = nums[pivot] : return pivot.

* If the target is not yet found :

* If target < nums[pivot], continue the search on the left right = pivot - 1.

* Else continue the search on the right left = pivot + 1.

## 278. First Bad Version

You are a product manager and currently leading a team to develop a new product. Unfortunately, the latest version of your product fails the quality check. Since each version is developed based on the previous version, all the versions after a bad version are also bad. Suppose you have n versions [1, 2, ..., n] and you want to find out the first bad one, which causes all the following ones to be bad. You are given an API bool isBadVersion(version) which returns whether version is bad. Implement a function to find the first bad version. You should minimize the number of calls to the API.

Example 1:

Input: n = 5, bad = 4

Output: 4

Explanation:

call isBadVersion(3) -> false

call isBadVersion(5) -> true

call isBadVersion(4) -> true

Then 4 is the first bad version.

Example 2:

Input: n = 1, bad = 1

Output: 1

Constraints:

1 <= bad <= n <= 2^31 - 1

### Answer 2

```javascript
var solution = function(isBadVersion) {
    /**
     * @param {integer} n Total versions
     * @return {integer} The first bad version
     */
    // [bad, bad]
    // 1,2,3,4,5
    return function(n) {
    // Initialize two pointers, pointer 1 at begining of versions (0), pointer 2 at end of version (n)
        let start = 0;
        let end = n;
        // Loop while the start position is less or equal to the end position
        while (start <= end) {
    // Find the middle point (We will use this to check which half of the list we will focus on next)
            let mid = Math.floor((start + end)/2)
    // If the bad version is at the mid point of the list, that means the first bad version is on the left,
    // reduce `end` to before mid point
            if (isBadVersion(mid)) {
                end = mid - 1;
            }else {
    // If the bad version is after the mid point of the list, that means the first bad version is on the right,
    // increase `start` to after mid point
                start = mid + 1
            }
        }
    // start will ways hold the first bad version
        return start;
    };
};


var solution = function(isBadVersion) {
    return function(n) {
        let start = 0;
        let end = n;
        while (start <= end) {
            let mid = Math.floor((start + end)/2)
            if (isBadVersion(mid)) {
                end = mid - 1;
            }else {
                start = mid + 1
            }
        }
        return start;
    };
};


var solution = function(isBadVersion) {
    var searchInsert = function(nums, target) {
    // o(n)
   for(let [i,num] of nums.entries()){
       if(num>=target) return i;
   }
   return nums.length   
  }

// Your input => 5
//               4
// Output => 4
// Expected => 4
```

## 35. Search Insert Position

Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order. You must write an algorithm with O(log n) runtime complexity.

Example 1:

Input: nums = [1,3,5,6], target = 5

Output: 2

Example 2:

Input: nums = [1,3,5,6], target = 2

Output: 1

Example 3:

Input: nums = [1,3,5,6], target = 7

Output: 4

Example 4:

Input: nums = [1,3,5,6], target = 0

Output: 0

Example 5:

Input: nums = [1], target = 0

Output: 0

Constraints:

1 <= nums.length <= 10^4

-10^4 <= nums[i] <= 10^4

nums contains distinct values sorted in ascending order.

-10^4 <= target <= 10^4

### Answer 3

```javascript
  var searchInsert = function(nums, target) {
    //o(log(n))
    let i=0,j=nums.length-1;
    let m=Math.floor((i+j)/2);
    while(nums[m]!==target && i<=j){
        if(nums[m]<target) i=m+1;
        else j=m-1;
        m=Math.floor((i+j)/2);
    }
    //if target is not in nums, after the loop, m=j=i-1; nums[j]<=target<=num[i]
    if (nums[m]===target) return m;
    return i;
};

// Your input => [1,3,5,6]
//               5
// Output => 2
// Expected => 2
```

## 977. Squares of a Sorted Array

Given an integer array nums sorted in *non-decreasing* order, return an array of the *squares of each number* sorted in non-decreasing order.

Example 1:

Input: nums = [-4,-1,0,3,10]

Output: [0,1,9,16,100]

Explanation: After squaring, the array becomes [16,1,0,9,100].

After sorting, it becomes [0,1,9,16,100].

Example 2:

Input: nums = [-7,-3,2,3,11]

Output: [4,9,9,49,121]

* 1 <= nums.length <= 10^4
* -104 <= nums[i] <= 104
* nums is sorted in non-decreasing order.

*Follow up*: Squaring each element and sorting the new array is very trivial, could you find an O(n) solution using a different approach?

### Answer 4

```javascript
var sortedSquares = function(nums) {
    let squared = [], l = 0, r = nums.length - 1;

    while (l <= r) {
        if (Math.abs(nums[l]) > Math.abs(nums[r]))
            squared.push(nums[l++] ** 2);
        else
            squared.push(nums[r--] ** 2);
    }
    return squared.reverse();
};

Your input
[-4,-1,0,3,10]
Output
[0,1,9,16,100]
Expected
[0,1,9,16,100]
```

## 189. Rotate Array

Given an array, rotate the array to the right by k steps, where k is non-negative.

Example 1:

Input: nums = [1,2,3,4,5,6,7], k = 3

Output: [5,6,7,1,2,3,4]

Explanation:

rotate 1 steps to the right: [7,1,2,3,4,5,6]

rotate 2 steps to the right: [6,7,1,2,3,4,5]

rotate 3 steps to the right: [5,6,7,1,2,3,4]

Example 2:

Input: nums = [-1,-100,3,99], k = 2

Output: [3,99,-1,-100]

Explanation:

rotate 1 steps to the right: [99,-1,-100,3]

rotate 2 steps to the right: [3,99,-1,-100]

Constraints:

1 <= nums.length <= 10^5
-2^31 <= nums[i] <= 2^31 - 1
0 <= k <= 10^5

### Answer 5

```javascript
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {void} Do not return anything, modify nums in-place instead.
 */
var rotate = function(nums, k) {
    k = k % nums.length;
    if (k === 0) {
        return nums;
    }
    
    nums.reverse();
    
    let l = 0;
    let r = k-1;
    while (l < r) {
        let temp = nums[l];
        nums[l] = nums[r];
        nums[r] = temp;
        l++;
        r--;
    }
    
    l = k;
    r = nums.length - 1;
    while (l < r) {
        let temp = nums[l];
        nums[l] = nums[r];
        nums[r] = temp;
        l++;
        r--;
    }
    
    return nums;
};

Your input
[1,2,3,4,5,6,7]
3
Output
[5,6,7,1,2,3,4]
Expected
[5,6,7,1,2,3,4]
```

## 283. Move Zeroes

Given an integer array nums, move all 0's to the end of it while maintaining the relative order of the non-zero elements.
Note that you must do this in-place without making a copy of the array.

Example 1:

Input: nums = [0,1,0,3,12]

Output: [1,3,12,0,0]

Example 2:

Input: nums = [0]

Output: [0]

Constraints:

1 <= nums.length <= 104

-231 <= nums[i] <= 231 - 1

### Answer 6

```javascript
var moveZeroes = function(nums) {
    let count=0;
    for(let i=0;i<nums.length;) {
        if(nums[i] == 0) {
            nums.splice(i,1);
            count++;
        } else {
            i++;
        }
    }
     for(let i=0;i<count;i++) {
            nums.push(0);
        }
};
Your input
[0,1,0,3,12]
Output
[1,3,12,0,0]
Expected
[1,3,12,0,0]

```

This question comes under a broad category of "Array Transformation". This category is the meat of tech interviews. Mostly because arrays are such a simple and easy to use data structure. Traversal or representation doesn't require any boilerplate code and most of your code will look like the Pseudocode itself.

The 2 requirements of the question are:

* Move all the 0's to the end of array.

* All the non-zero elements must retain their original order.

It's good to realize here that both the requirements are mutually exclusive, i.e., you can solve the individual sub-problems and then combine them for the final solution.

## 167. Two Sum II - Input array is sorted

Given a **1-indexed** array of integers *numbers* that is already **sorted in non-decreasing order**, find two numbers such that they add up to a specific *target* number. Let these two numbers be *numbers[index1]* and *numbers[index2]* where *1 <= first < second <= numbers.length*.

Return the indices of the two numbers, *index1* and *index2*, as an integer array *[index1, index2]* of length 2.

The tests are generated such that there is **exactly one solution**. You **may not** use the same element twice.

Example 1:

Input: numbers = [2,7,11,15], target = 9

Output: [1,2]

Explanation: The sum of 2 and 7 is 9. Therefore index1 = 1, index2 = 2.

Example 2:

Input: numbers = [2,3,4], target = 6

Output: [1,3]

Explanation: The sum of 2 and 4 is 6. Therefore index1 = 1, index2 = 3.

Example 3:

Input: numbers = [-1,0], target = -1

Output: [1,2]

Explanation: The sum of -1 and 0 is -1. Therefore index1 = 1, index2 = 2.

Constraints:

2 <= numbers.length <= 3 * 10^4

-1000 <= numbers[i] <= 1000

numbers is sorted in non-decreasing order.

-1000 <= target <= 1000

The tests are generated such that there is exactly one solution.

```javascript
var twoSum = function(numbers, target) {
    let comp = {};

    for (let i = 0; i < numbers.length; ++i) {
        if (comp[numbers[i]] > 0) {
          return [comp[numbers[i]], i + 1];
        }
        comp[target - numbers[i]] = i + 1;
    }
};

Your input
[2,7,11,15]
9
Output
[1,2]
Expected
[1,2]
```

## 344. Reverse String

Write a function that reverses a string. The input string is given as an array of characters *s*.

Example 1:

Input: s = ["h","e","l","l","o"]

Output: ["o","l","l","e","h"]

Example 2:

Input: s = ["H","a","n","n","a","h"]

Output: ["h","a","n","n","a","H"]

Constraints:

1 <= s.length <= 10^5

s[i] is a printable ascii character.

**Follow up**: Do not allocate extra space for another array. You must do this by modifying the input array *in-place* with *O(1)* extra memory.

```javascript
var reverseString = function(s) {    
    var i = 0;
    var j = s.length - 1;
    var temp;
    
    while (i < j) {
        temp = s[i];
        s[i] = s[j];
        s[j] = temp;  
        i++;
        j--;
    }
   
    return s;
};


Your input
["h","e","l","l","o"]
Output
["o","l","l","e","h"]
Expected
["o","l","l","e","h"]
```
