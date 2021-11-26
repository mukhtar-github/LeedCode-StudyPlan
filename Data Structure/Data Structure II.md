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

### 75. Sort Colors

Given an array nums with n objects colored red, white, or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white, and blue.

We will use the integers 0, 1, and 2 to represent the color red, white, and blue, respectively.
You must solve this problem without using the library's sort function.

Example 1:

Input: nums = [2,0,2,1,1,0]

Output: [0,0,1,1,2,2]

Example 2:

Input: nums = [2,0,1]

Output: [0,1,2]

Example 3:

Input: nums = [0]

Output: [0]

Example 4:

Input: nums = [1]

Output: [1]

Constraints:

* n == nums.length
* 1 <= n <= 300
* nums[i] is 0, 1, or 2.

Follow up: Could you come up with a one-pass algorithm using only constant extra space?

#### Answer 4

```javascript
var sortColors = function(nums) {
    let low= 0, high= nums.length- 1, mid= 0, temp= 0;
    
    while(mid <= high) {
        if(nums[mid] === 0) {
            // swap mid and low pointers values
            temp= nums[low];
            nums[low] = nums[mid];
            nums[mid]= temp;
            
            low++;
            mid++;
        } else if(nums[mid] === 2) {
            // swap mid and high pointers values
            temp= nums[high];
            nums[high]= nums[mid];
            nums[mid]= temp;
            
            high--;
        } else {
            mid++
        }
    }
    
    return nums;
};

//Your input
[2,0,2,1,1,0]
//Output
[0,0,1,1,2,2]
//Expected
[0,0,1,1,2,2]
```

### 56. Merge Intervals

Given an array of intervals where intervals[i] = [starti, endi], merge all overlapping intervals, and return an array of the non-overlapping intervals that cover all the intervals in the input.

Example 1:

Input: intervals = [[1,3],[2,6],[8,10],[15,18]]

Output: [[1,6],[8,10],[15,18]]

Explanation: Since intervals [1,3] and [2,6] overlaps, merge them into [1,6].

Example 2:

Input: intervals = [[1,4],[4,5]]

Output: [[1,5]]

Explanation: Intervals [1,4] and [4,5] are considered overlapping.

Constraints:

* 1 <= intervals.length <= 10^4
* intervals[i].length == 2
* 0 <= starti <= endi <= 10^4

#### Answer 5

```javascript
var merge = function(intervals) {
    
    if(intervals.length <2){
        return intervals;
    }
    
    // sort intervals    
    const sortedIntervals = intervals.sort((a,b) => {
        return a[0]-b[0];
    });
    
    
    let stack = [];
    stack.push(sortedIntervals[0]);
    
    for(let i=1;i<sortedIntervals.length;i++){
        let currStartTime = sortedIntervals[i][0];
        let currEndTime = sortedIntervals[i][1];
        let prevStartTime = stack[stack.length-1][0];
        let prevEndTime = stack[stack.length-1][1];
        
        if(currStartTime <= prevEndTime){
            stack[stack.length-1] = [Math.min(currStartTime,prevStartTime),Math.max(prevEndTime,currEndTime)];
        }
        else {
            stack.push(sortedIntervals[i]);
        }
    }
    return stack;
};

//Your input
[[1,3],[2,6],[8,10],[15,18]]
//Output
[[1,6],[8,10],[15,18]]
//Expected
[[1,6],[8,10],[15,18]]
```

### 706. Design HashMap

Design a HashMap without using any built-in hash table libraries.

Implement the MyHashMap class:

MyHashMap() initializes the object with an empty map.
void put(int key, int value) inserts a (key, value) pair into the HashMap. If the key already exists in the map, update the corresponding value.
int get(int key) returns the value to which the specified key is mapped, or -1 if this map contains no mapping for the key.
void remove(key) removes the key and its corresponding value if the map contains the mapping for the key.

Example 1:

Input

["MyHashMap", "put", "put", "get", "get", "put", "get", "remove", "get"]

[[], [1, 1], [2, 2], [1], [3], [2, 1], [2], [2], [2]]

Output

[null, null, null, 1, -1, null, 1, null, -1]

Explanation

MyHashMap myHashMap = new MyHashMap();

myHashMap.put(1, 1); // The map is now [[1,1]]

myHashMap.put(2, 2); // The map is now [[1,1], [2,2]]

myHashMap.get(1);    // return 1, The map is now [[1,1], [2,2]]

myHashMap.get(3);    // return -1 (i.e., not found), The map is now [[1,1], [2,2]]

myHashMap.put(2, 1); // The map is now [[1,1], [2,1]] (i.e., update the existing value)

myHashMap.get(2);    // return 1, The map is now [[1,1], [2,1]]

myHashMap.remove(2); // remove the mapping for 2, The map is now [[1,1]]

myHashMap.get(2);    // return -1 (i.e., not found), The map is now [[1,1]]

Constraints:

* 0 <= key, value <= 10^6
* At most 10^4 calls will be made to put, get, and remove.

#### Answer 6

```javascript
/*

var MyHashMap = function() {
    
};

/** 
 * @param {number} key 
 * @param {number} value
 * @return {void}
 */
MyHashMap.prototype.put = function(key, value) {
    
};

/** 
 * @param {number} key
 * @return {number}
 */
MyHashMap.prototype.get = function(key) {
    
};

/** 
 * @param {number} key
 * @return {void}
 */
MyHashMap.prototype.remove = function(key) {
    
};

/** 
 * Your MyHashMap object will be instantiated and called as such:
 * var obj = new MyHashMap()
 * obj.put(key,value)
 * var param_2 = obj.get(key)
 * obj.remove(key)
 */*/


class ListNode {
    constructor(key, val, next) {
        this.key = key
        this.val = val
        this.next = next
    }
}
class MyHashMap {
    constructor() {
        this.size = 19997
        this.mult = 12582917
        this.data = new Array(this.size)
    }
    hash(key) {
        return key * this.mult % this.size
    }
    put(key, val) {
        this.remove(key)
        let h = this.hash(key)
        let node = new ListNode(key, val, this.data[h])
        this.data[h] = node
    }
    get(key) {
        let h = this.hash(key), node = this.data[h]
        for (; node; node = node.next)
            if (node.key === key) return node.val
        return -1
    }
    remove(key) {
        let h = this.hash(key), node = this.data[h]
        if (!node) return
        if (node.key === key) this.data[h] = node.next
        else for (; node.next; node = node.next)
            if (node.next.key === key) {
                node.next = node.next.next
                return
            }
    }
};

//Your input
["MyHashMap","put","put","get","get","put","get","remove","get"]
[[],[1,1],[2,2],[1],[3],[2,1],[2],[2],[2]]
//Output
[null,null,null,1,-1,null,1,null,-1]
//Expected
[null,null,null,1,-1,null,1,null,-1]
```

### 119. Pascal's Triangle II

#### Answer 7

Given an integer *rowIndex*, return the *rowIndex^th* (*0-indexed*) row of the *Pascal's triangle*.

In *Pascal's triangle*, each number is the sum of the two numbers directly above it as shown:

Example 1:

Input: rowIndex = 3

Output: [1,3,3,1]

Example 2:

Input: rowIndex = 0

Output: [1]

Example 3:

Input: rowIndex = 1

Output: [1,1]

Constraints:

* 0 <= rowIndex <= 33

Follow up: Could you optimize your algorithm to use only O(rowIndex) extra space?

```javascript

    

//Your input
["MyHashMap","put","put","get","get","put","get","remove","get"]
[[],[1,1],[2,2],[1],[3],[2,1],[2],[2],[2]]
//Output
[null,null,null,1,-1,null,1,null,-1]
//Expected
[null,null,null,1,-1,null,1,null,-1]
```
