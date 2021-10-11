# Algorithm II

## Binary Search

### 34. Find First and Last Position of Element in Sorted Array

Given an array of integers nums sorted in ascending order, find the starting and ending position of a given target value.

If target is not found in the array, return [-1, -1].

You must write an algorithm with O(log n) runtime complexity.

Example 1:

Input: nums = [5,7,7,8,8,10], target = 8

Output: [3,4]

Example 2:

Input: nums = [5,7,7,8,8,10], target = 6

Output: [-1,-1]

Example 3:

Input: nums = [], target = 0

Output: [-1,-1]

Constraints:

* 0 <= nums.length <= 105
* -109 <= nums[i] <= 109
* nums is a non-decreasing array.
* -10^9 <= target <= 10^9

#### Answer 1

```javascript
var searchRange = function(nums, target) {
  let low= 0 ;
    let right = nums.length-1;
    
    let start = null
    let end =null;

    while(low<=right){
        
        let mid = low  + Math.floor((right-low)/2);
        
        if(nums[mid] == target){
            start= mid;
        }
        
        if(nums[mid]< target){
            low = mid+1
           
        }else{
            right = mid-1
        }
    }
   
    if(start==null ) return [-1, -1];
    
    right = nums.length-1;
    
    while(nums[low]===target && low<=right){
        end = low
       low++
    }
    
  
    return [start, end];  
};

var searchRange = function(nums, target) {
    let first = nums.indexOf(target)
    let last = nums.lastIndexOf(target)
    return [first, last]
};

//Your input
[5,7,7,8,8,10]
8
//Output
[3,4]
//Expected
[3,4]
```

### 33. Search in Rotated Sorted Array

There is an integer array nums sorted in ascending order (with **distinct** values).

Prior to being passed to your function, *nums* is possibly rotated at an unknown pivot index *k (1 <= k < nums.length)* such that the resulting array is *[nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]* (**0-indexed**). For example, *[0,1,2,4,5,6,7]* might be rotated at pivot index *3* and become *[4,5,6,7,0,1,2]*.

Given the array *nums* **after** the possible rotation and an integer *target*, return the index of *target* if it is in *nums*, or *-1* if it is not in *nums*.

You must write an algorithm with *O(log n)* runtime complexity.

Example 1:

Input: nums = [4,5,6,7,0,1,2], target = 0

Output: 4

Example 2:

Input: nums = [4,5,6,7,0,1,2], target = 3

Output: -1

Example 3:

Input: nums = [1], target = 0

Output: -1

Constraints:

* 1 <= nums.length <= 5000
* -10^4 <= nums[i] <= 10^4
* All values of nums are unique.
* nums is an ascending array that is possibly rotated.
* -10^4 <= target <= 10^4

```javascript
var search = function(nums, target) {
    for(let i = 0; i < nums.length; i++){
        if(nums[i] === target) return i
    }
    return -1
};

//Your input
[4,5,6,7,0,1,2]
0
//Output
4
//Expected
4
```
