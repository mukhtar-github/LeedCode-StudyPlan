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

There is an integer array *nums* sorted in ascending order (with **distinct** values).

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

#### Answer 2

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

### 74. Search a 2D Matrix

Write an efficient algorithm that searches for a value in an *m x n* matrix. This matrix has the following properties:

* Integers in each row are sorted from left to right.
* The first integer of each row is greater than the last integer of the previous row.

Example 1:

![mat](https://assets.leetcode.com/uploads/2020/10/05/mat.jpg)

Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3

Output: true

Example 2:

![mat2](https://assets.leetcode.com/uploads/2020/10/05/mat2.jpg)

Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 13

Output: false

Constraints:

* m == matrix.length
* n == matrix[i].length
* 1 <= m, n <= 100
* -10^4 <= matrix[i][j], target <= 10^4

#### Answer 3

```javascript
var searchMatrix = function(matrix, target) {
    let colEnd=matrix[0].length-1;
    let rowStart=0;let rowEnd=matrix.length-1;
    while(rowStart<=rowEnd){
        if(matrix[rowStart][colEnd]>=target){
            if(matrix[rowStart][colEnd]===target){
                return true
            }else {
                colEnd--;
            }
        }else{
            rowStart++;
        }
    }
    return false;
};

//Your input
[[1,3,5,7],[10,11,16,20],[23,30,34,60]]
3
//Output
true
//Expected
true
```

### 153. Find Minimum in Rotated Sorted Array

Suppose an array of length *n* sorted in ascending order is **rotated** between *1 and n* times. For example, the array *nums = [0,1,2,4,5,6,7]* might become:

* *[4,5,6,7,0,1,2]* if it was rotated *4* times.
* *[0,1,2,4,5,6,7]* if it was rotated *7* times.

Notice that **rotating** an array *[a[0], a[1], a[2], ..., a[n-1]]* 1 time results in the array *[a[n-1], a[0], a[1], a[2], ..., a[n-2]]*.

Given the sorted rotated array nums of unique elements, return the minimum element of this array.

You must write an algorithm that runs in *O(log n) time*.

Example 1:

Input: nums = [3,4,5,1,2]

Output: 1

Explanation: The original array was [1,2,3,4,5] rotated 3 times.

Example 2:

Input: nums = [4,5,6,7,0,1,2]

Output: 0

Explanation: The original array was [0,1,2,4,5,6,7] and it was rotated 4 times.

Example 3:

Input: nums = [11,13,15,17]

Output: 11

Explanation: The original array was [11,13,15,17] and it was rotated 4 times.

Constraints:

* n == nums.length
* 1 <= n <= 5000
* -5000 <= nums[i] <= 5000
* All the integers of nums are unique.
* nums is sorted and rotated between 1 and n times.

#### Answer 4

```javascript
var findMin = function(nums) {
    let start=0, end= nums.length-1, mid= Math.floor((start+end)/2);
    
    while( start <= end ){
        //If nums is not rotated
        if (nums[end] >= nums[start]){
            return nums[start];
        }
        
        //With this, we will return something for sure before exiting the while loop
        if (end-start == 1){
            return nums[end];
        }
        
        if (nums[mid] <= nums[start]){
            end = mid;
        }
        else {
            start = mid;
        }
        
        mid = Math.floor((start+end)/2);
    }
};

//Your input
[3,4,5,1,2]
//Output
1
//Expected
1
```

### 162. Find Peak Element

peak element is an element that is strictly greater than its neighbors.

Given an integer array *nums*, find a peak element, and return its index. If the array contains multiple peaks, return the index to **any of the peaks**.

You may imagine that *nums[-1] = nums[n] = -∞*.

You must write an algorithm that runs in *O(log n)* time.

Example 1:

Input: nums = [1,2,3,1]

Output: 2

Explanation: 3 is a peak element and your function should return the index number 2.

Example 2:

Input: nums = [1,2,1,3,5,6,4]

Output: 5

Explanation: Your function can return either index number 1 where the peak element is 2, or index number 5 where the peak element is 6.

Constraints:

* 1 <= nums.length <= 1000
* -231 <= nums[i] <= 231 - 1
* nums[i] != nums[i + 1] for all valid i.

#### Answer 5

```javascript
var findPeakElement = function(nums) {
    let left = 0, right = nums.length-1, mid;
    
    while(left < right) {
        mid = Math.floor((right+left)/2);
        if(nums[mid] > nums[mid+1]) right = mid;
        else left = mid+1;
    }
    return left;
};

//Your input
[1,2,3,1]
//Output
2
//Expected
2
```

## Two Pointers

### 82. Remove Duplicates from Sorted List II

Given the *head* of a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list. Return the linked list **sorted** as well.

Example 1:

![linkedlist1](https://assets.leetcode.com/uploads/2021/01/04/linkedlist1.jpg)

Input: head = [1,2,3,3,4,4,5]

Output: [1,2,5]

Example 2:

![linkedlist2](https://assets.leetcode.com/uploads/2021/01/04/linkedlist2.jpg)

Input: head = [1,1,1,2,3]

Output: [2,3]

Constraints:

* The number of nodes in the list is in the range [0, 300].
* -100 <= Node.val <= 100
* The list is guaranteed to be *sorted* in ascending order.

#### Answer 6

```javascript
var deleteDuplicates = function(head) {
    if (!head || !head.next) return head
    let previous = null
    const newNode = new ListNode()
    let dummy = newNode
    while (head) {
        const next = head.next ? head.next.val : null
        if (head.val !== previous && head.val !== next) {
            dummy.next = new ListNode(head.val)
            dummy = dummy.next
        }
        previous = head.val
        head = head.next 
    }
    return newNode.next
};

const deleteDuplicates = (head) => {
    const res = new ListNode(-1)
    let last = res
    let dupe = null
    let curr = head
    while (curr) {
        const next = curr.next
        if (!next) {
            if (curr.val !== dupe) {
                last.next = curr
            }
            break
        }
        if (curr.val === next.val || curr.val === dupe) {
            dupe = curr.val
            curr = curr.next
        } else {
            last.next = curr
            last = curr
            curr = curr.next
            last.next = null
        }
    }
    return res.next
};

//Your input
[1,2,3,3,4,4,5]
//Output
[1,2,5]
//Expected
[1,2,5]
```

### 15. 3Sum

Given an integer array nums, return all the triplets *[nums[i], nums[j], nums[k]]* such that *i != j, i != k*, and *j != k*, and *nums[i] + nums[j] + nums[k] == 0*.

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
* -10^5 <= nums[i] <= 10^5

#### Answer 7

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

### 844. Backspace String Compare

Given two strings *s* and *t*, return *true* if they are equal when both are typed into empty text editors. *'#'* means a backspace character.

Note that after backspacing an empty text, the text will continue empty.

Example 1:

Input: s = "ab#c", t = "ad#c"

Output: true

Explanation: Both s and t become "ac".

Example 2:

Input: s = "ab##", t = "c#d#"

Output: true

Explanation: Both s and t become "".

Example 3:

Input: s = "a##c", t = "#a#c"

Output: true

Explanation: Both s and t become "c".

Example 4:

Input: s = "a#c", t = "b"

Output: false

Explanation: s becomes "c" while t becomes "b".

Constraints:

* 1 <= s.length, t.length <= 200
* s and t only contain lowercase letters and '#' characters.

Follow up: Can you solve it in O(n) time and O(1) space?

#### Answer 8

```javascript

```
