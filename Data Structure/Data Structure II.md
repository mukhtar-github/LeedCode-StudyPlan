# Data Structure II

## Array

### 136. Single Number

Given a *non-empty* array of integers nums, every element appears twice except for one. Find that single one.

You must implement a solution with a linear runtime complexity and use only constant extra space.

Example 1:

Input: nums = [2,2,1]

Output: 1

Example 2:

Input: nums = [4,1,2,1,2]

Output: 4

Example 3:

Input: nums = [1]

Output: 1

Constraints:

* 1 <= nums.length <= 3 * 10^4
* -3 x 104 <= nums[i] <= 3 x 10^4
* Each element in the array appears twice except for one element which appears only once.

#### Answer 1

```javascript
var singleNumber = function(nums) {
    let single = 0;
    for (let num of nums) {
        single ^= num
    }
    return single
};


//Your input
[2,2,1]
//Output
1
//Expected
1
```

### 169. Majority Element

Given an array *nums* of size *n*, return the majority element.

The majority element is the element that appears more than *⌊n / 2⌋* times. You may assume that the majority element always exists in the array.

Example 1:

Input: nums = [3,2,3]

Output: 3

Example 2:

Input: nums = [2,2,1,1,1,2,2]

Output: 2

Constraints:

* n == nums.length
* 1 <= n <= 5 * 10^4
* -231 <= nums[i] <= 231 - 1

Follow-up: Could you solve the problem in linear time and in O(1) space?

#### Answer 2

```javascript
var majorityElement = function(nums) {
    const criterion = nums.length / 2 >> 0
    const countMap = new Map()
    for (const num of nums) {
        const curNum = (countMap.get(num) ?? 0) + 1
        if (curNum > criterion)
            return num
        countMap.set(num, curNum)
    }
};

//Your input
[3,2,3]
//Output
3
//Expected
3
```

### 15. 3Sum

Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.

Notice that the solution set must not contain duplicate triplets.

Example 1:

Input: nums = [-1,0,1,2,-1,-4]

Output: [[-1,-1,2],[-1,0,1]]

Example 2:

Input: nums = []

Output: []

Example 3:

Input: nums = [0]

Output: []

Constraints:

* 0 <= nums.length <= 3000
* -105 <= nums[i] <= 10^5

#### Answer 3

```javascript
var threeSum = function(nums) {
    var res = [];
    if(!nums || !nums.length) return res;

    nums = nums.sort((a, b) => a - b);

    for(let i=0; i<nums.length - 2; i++){
        while(nums[i-1] === nums[i]) i++;
        
        let j=i+1, k=nums.length-1;
        while(j<k){
            let sum = nums[i] + nums[j] + nums[k];
            if(sum === 0){
                res.push([nums[i],nums[j],nums[k]]);
                while (nums[j] === nums[j + 1]) j++;
                while (nums[k] === nums[k-1]) k--;
            }
            //searching for -nums[i]
            if(sum > 0){
                k--;
            }else{
                j++;
            }            
        }
    }
    return res;
};

//Your input
[-1,0,1,2,-1,-4]
//Output
[[-1,-1,2],[-1,0,1]]
//Expected
[[-1,-1,2],[-1,0,1]]
```
