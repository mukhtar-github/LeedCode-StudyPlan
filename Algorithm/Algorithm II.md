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
var backspaceCompare = function (s, t) {
    const string1 = [];
    const string2 = [];

    function createArrayOfString(string, array) {
        for (const char of string) {
            if (char === "#") {
                array.pop();
            } else {
                array.push(char);
            }
        }
    }

    createArrayOfString(s, string1);
    createArrayOfString(t, string2);

    if (string1.length !== string2.length) return false;
    for (let i = 0; i < string1.length; i++) {
        if (string1[i] !== string2[i]) return false;
    }
    return true;
};

//Your input
"ab#c"
"ad#c"
//Output
true
//Expected
true
```

### 986. Interval List Intersections

You are given two lists of closed intervals, firstList and secondList, where firstList[i] = [starti, endi] and secondList[j] = [startj, endj]. Each list of intervals is pairwise *disjoint* and in *sorted order*.

Return the intersection of these two interval lists.

A *closed interval* [a, b] (with a <= b) denotes the set of real numbers x with a <= x <= b.

The *intersection* of two closed intervals is a set of real numbers that are either empty or represented as a closed interval. For example, the intersection of [1, 3] and [2, 4] is [2, 3].

Example 1:

![interval1](https://assets.leetcode.com/uploads/2019/01/30/interval1.png)

Input: firstList = [[0,2],[5,10],[13,23],[24,25]], secondList = [[1,5],[8,12],[15,24],[25,26]]

Output: [[1,2],[5,5],[8,10],[15,23],[24,24],[25,25]]

Example 2:

Input: firstList = [[1,3],[5,9]], secondList = []

Output: []

Example 3:

Input: firstList = [], secondList = [[4,8],[10,12]]

Output: []

Example 4:

Input: firstList = [[1,7]], secondList = [[3,10]]

Output: [[3,7]]

Constraints:

* 0 <= firstList.length, secondList.length <= 1000
* firstList.length + secondList.length >= 1
* 0 <= starti < endi <= 10^9
* endi < starti+1
* 0 <= startj < endj <= 10^9
* endj < startj+1

```javascript
var intervalIntersection = function(firstList, secondList) {
    const intersect = [];
    let itr1 = 0, itr2 = 0;
    while(itr1 < firstList.length && itr2 < secondList.length) {
        const interval1 = firstList[itr1],
              interval2 = secondList[itr2];

// if interval1 and interval2 overlap, add the intersected interval
        if((interval1[0] >= interval2[0] && interval1[0] <= interval2[1]) ||
          (interval2[0] >= interval1[0] && interval2[0] <= interval1[1])) {
            intersect.push([Math.max(interval1[0], interval2[0]), Math.min(interval1[1], interval2[1])]);
        }
        
// if the interval1 is ended before interval2, move to the next interval in the first list (means that interval is completely processed)
        if(interval1[1] < interval2[1]) {
            ++itr1;
        } else {  // if the interval2 is ended before interval1, move to the next interval in the second list
            ++itr2;
        }
    }
    return intersect;
};

var intervalIntersection = function(A, B) {
    const result = []
    let currA = 0;
    let currB = 0;
    
    while(currA < A.length && currB < B.length) {
        const [startA, endA] = A[currA];
        const [startB, endB] = B[currB];
        
        const overlapStart = Math.max(startA, startB);
        const overlapEnd = Math.min(endA, endB);
        
        if(overlapStart <= overlapEnd) result.push([overlapStart, overlapEnd])
        
        if(endA < endB) currA++;
        else if (endB < endA) currB++;
        else {
            currA++;
            currB++;
        }
    }
    return result;    
};

//Time Complexity = O(n)
//Space Complexity = O(n)

//Your input
[[0,2],[5,10],[13,23],[24,25]]
[[1,5],[8,12],[15,24],[25,26]]
//Output
[[1,2],[5,5],[8,10],[15,23],[24,24],[25,25]]
//Expected
[[1,2],[5,5],[8,10],[15,23],[24,24],[25,25]]
```

### 11. Container With Most Water

Given *n* non-negative integers *a1, a2, ..., an* , where each represents a point at coordinate *(i, ai)*. *n* vertical lines are drawn such that the two endpoints of the line *i* is at *(i, ai)* and *(i, 0)*. Find two lines, which, together with the x-axis forms a container, such that the container contains the most water.

**Notice** that you may not slant the container.

Example 1:

![question_11](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg)

Input: height = [1,8,6,2,5,4,8,3,7]

Output: 49

Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.

Example 2:

Input: height = [1,1]

Output: 1

Example 3:

Input: height = [4,3,2,1,4]

Output: 16

Example 4:

Input: height = [1,2,1]

Output: 2

Constraints:

* n == height.length
* 2 <= n <= 10^5
* 0 <= height[i] <= 10^4

#### Answer 9

```javascript
const maxArea = (H) => {
  let left = 0, right = H.length - 1, max = 0;
  while (left < right) {
    max = Math.max(max, Math.min(H[left], H[right]) * (right - left));
    if (H[left] < H[right]) left++; // Left is smaller, try a new left line
    else right--; // Right is smaller, try a new right line
  }
  return max;
};

//Your input
[1,8,6,2,5,4,8,3,7]
//Output
49
//Expected
49

var maxArea = function(H) {
    let ans = 0, i = 0, j = H.length-1
    while (i < j) {
        ans = Math.max(ans, Math.min(H[i], H[j]) * (j - i))
        H[i] <= H[j] ? i++ : j--
    }
    return ans
};
```

## Sliding Window

### 438. Find All Anagrams in a String

Given two strings *s* and *p*, return an array of all the start indices of *p*'s anagrams in *s*. You may return the answer in **any order**.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

Example 1:

Input: s = "cbaebabacd", p = "abc"

Output: [0,6]

Explanation:

The substring with start index = 0 is "cba", which is an anagram of "abc".

The substring with start index = 6 is "bac", which is an anagram of "abc".

Example 2:

Input: s = "abab", p = "ab"

Output: [0,1,2]

Explanation:

The substring with start index = 0 is "ab", which is an anagram of "ab".

The substring with start index = 1 is "ba", which is an anagram of "ab".

The substring with start index = 2 is "ab", which is an anagram of "ab".

Constraints:

* 1 <= s.length, p.length <= 3 * 10^4
* s and p consist of lowercase English letters.

#### Answer 10

```javascript
var findAnagrams = function(s, p) {
    let sChars = new Array(26).fill(0);
    let pChars = new Array(26).fill(0);
    let left = 0, ch;
    let pLength = p.length;
    
    for (let i = 0; i < p.length; i++) {
        let index = p[i].charCodeAt(0) - 97;
        pChars[index] += 1;
    }
    
    let result = [];
    
    for (let i=0; i< s.length; i++) {
        let index = s[i].charCodeAt(0) - 97;
        sChars[index] += 1;
        
        if((i-left) >= pLength) {
            ch = s.charAt(left).charCodeAt(0) - 97;
             if(sChars[ch] === 1) {
                 sChars[ch] = 0;
             } else {
                 sChars[ch] -= 1;
             }
            left++;
        }
        
        if(areArrayEqual(sChars, pChars)) {
            result.push(i - pLength + 1);
        }
    }
    
    return result;
};

//Your input
"cbaebabacd"
"abc"
//Output
[0,6]
//Expected
[0,6]

function areArrayEqual(arr1, arr2) {
    if (arr1.length !== arr2.length) return false;
    let j = 0;
    let bool = true;
    for (let i = 0; i < arr1.length; i++) {
            if (arr1[i] !== arr2[j]) {
                bool = false;
            }
        j++;
    }
    return bool;
};


var findAnagrams = function(s2, s1) {
  let map = {},
        start = 0,
        matched = 0,
        res = [];

    for (let i = 0; i < s1.length; i ++) {
        let char = s1[i];
        if(!(char in map)) map[char] = 0;
        map[char] ++;
    }

    for (let end = 0; end < s2.length; end ++) {

        let right = s2[end];

        if (right in map) {
            map[right] --;
            if (map[right] === 0) matched ++;
        }

        if (matched === Object.keys(map).length) res.push(start);

        if (end >= s1.length - 1) {
            let left = s2[start];
            start ++;
            if(left in map) {
                if (map[left] === 0) matched --;
                map[left] ++;
            }
        }
    }
    return res;
};
```

### 713. Subarray Product Less Than K

Given an array of integers *nums* and an integer *k*, return the number of contiguous subarrays where the product of all the elements in the subarray is strictly less than *k*.

Example 1:

Input: nums = [10,5,2,6], k = 100

Output: 8

Explanation: The 8 subarrays that have product less than 100 are:
[10], [5], [2], [6], [10, 5], [5, 2], [2, 6], [5, 2, 6]

Note that [10, 5, 2] is not included as the product of 100 is not strictly less than k.

Example 2:

Input: nums = [1,2,3], k = 0

Output: 0

Constraints:

* 1 <= nums.length <= 3 * 10^4
* 1 <= nums[i] <= 1000
* 0 <= k <= 10^6

#### Answer 11

```javascript
var numSubarrayProductLessThanK = function(nums, k) {
    
    let count = 0
    let j = 0
    let i = 0
    let product = 1
   
    while (i < nums.length && j < nums.length) {
        if (product * nums[i] < k) {
            product = product * nums[i]
            count   = count + (i - j + 1)
            i++
        } else {
            if (nums[j]) product = product / nums[j]
            j++
        }
    }
    
    return count
};

//Your input
[10,5,2,6]
100
//Output
8
//Expected
8
```

### 209. Minimum Size Subarray Sum

Given an array of positive integers *nums* and a positive integer *target*, return the minimal length of a **contiguous subarray** *[numsl, numsl+1, ..., numsr-1, numsr]* of which the sum is greater than or equal to *target*. If there is no such subarray, return *0* instead.

Example 1:

Input: target = 7, nums = [2,3,1,2,4,3]

Output: 2

Explanation: The subarray [4,3] has the minimal length under the problem constraint.

Example 2:

Input: target = 4, nums = [1,4,4]

Output: 1

Example 3:

Input: target = 11, nums = [1,1,1,1,1,1,1,1]

Output: 0

Constraints:

* 1 <= target <= 109
* 1 <= nums.length <= 10^5
* 1 <= nums[i] <= 10^5

Follow up: If you have figured out the O(n) solution, try coding another solution of which the time complexity is O(n log(n)).

#### Answer 12

```javascript
var minSubArrayLen = function(target, nums) {
    let start = 0
    let end = 0
    let sum = nums[0];
    let flag = false
    let length = nums.length;
    while(end < nums.length){
        if(sum >= target){
            if(length > end - start+1) {
                length = end - start+1;
               }
            sum -= nums[start]
            flag = true
            start++
        }else {
            end++
            sum += nums[end]  
        }
       
   }
    if(!flag){
        return 0
       }
   return length
};

//Your input
7
[2,3,1,2,4,3]
//Output
2
//Expected
2
```

## Breadth-First Search / Depth-First Search

### 200. Number of Islands

Given an *m x n* 2D binary grid *grid* which represents a map of *'1'*s (land) and *'0'*s (water), return the number of islands.

An **island** is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

Example 1:

Input: grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]

Output: 1

Example 2:

Input: grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]

Output: 3

Constraints:

* m == grid.length
* n == grid[i].length
* 1 <= m, n <= 300
* grid[i][j] is '0' or '1'.

#### Answer 13

```javascript
var numIslands = function(grid) {
    var num_islands = 0
    for(var i=0;i<grid.length;i++) {
        for(var j=0;j<grid[i].length;j++) {
           if(grid[i][j] == "1") {
                //found land
                num_islands++
                dfs(grid,i,j)
            }
        }
    }
    return num_islands
};
var dfs = function(grid,row,col) {
    var numOfRows = grid.length;
    var numOfCols = grid[0].length;
    if (row < 0 || col < 0 || row >= numOfRows || col >= numOfCols || grid[row][col] == '0') {
      return;
    }

    grid[row][col] = '0';
    dfs(grid, row - 1, col);
    dfs(grid, row + 1, col);
    dfs(grid, row, col - 1);
    dfs(grid, row, col + 1);
}

//Your input
[["1","1","1","1","0"],["1","1","0","1","0"],["1","1","0","0","0"],["0","0","0","0","0"]]
//Output
1
//Expected
1
```

### 547. Number of Provinces

There are *n* cities. Some of them are connected, while some are not. If city *a* is connected directly with city *b*, and city *b* is connected directly with city *c*, then city *a* is connected indirectly with city *c*.

A **province** is a group of directly or indirectly connected cities and no other cities outside of the group.

You are given an *n x n* matrix *isConnected* where *isConnected[i][j] = 1* if the *ith* city and the *jth* city are directly connected, and *isConnected[i][j] = 0* otherwise.

Return the total number of **provinces**.

Example 1:

![graph1](https://assets.leetcode.com/uploads/2020/12/24/graph1.jpg)

Input: isConnected = [[1,1,0],[1,1,0],[0,0,1]]

Output: 2

Example 2:

![graph2](https://assets.leetcode.com/uploads/2020/12/24/graph2.jpg)

Input: isConnected = [[1,0,0],[0,1,0],[0,0,1]]
Output: 3

Constraints:

* 1 <= n <= 200
* n == isConnected.length
* n == isConnected[i].length
* isConnected[i][j] is 1 or 0.
* isConnected[i][i] == 1
* isConnected[i][j] == isConnected[j][i]

#### Answer 14

```javascript
// Idea: Every time we encounter 1, we need to find the connected component starting from this node. 
// Why? 1 means that this person is a direct friend of mine. 
// Now we want to visit all of his friends, all of his friends' friends and so on because all these people are my indirect friends and we together make one circle.

var findCircleNum = function(M) {
    if (M.length == 0 || M[0].length == 0) return 0;
    let circles = 0;
    let visited = new Array(M.length).fill(false);
    for (let vertex = 0; vertex < M.length; vertex++) {
        if (!visited[vertex]) {
            dfs(vertex, M, visited);
            circles++;
        }
    }
    return circles;
    // Time Complexity: O(N^2), we visit every node once
    // Space Complexity: O(N), for "visited" array
};

function dfs(vertex, grid, visited) {
    visited[vertex] = true;
    
    for (let to = 0; to < grid[vertex].length; to++) {
        if (grid[vertex][to] == 1 && !visited[to]) {
            dfs(to, grid, visited);
        }
    }
}

//Your input
[[1,1,0],[1,1,0],[0,0,1]]
//Output
2
//Expected
2
```

### 117. Populating Next Right Pointers in Each Node II

Given a binary tree

```java
struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
```

Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to *NULL*.

Initially, all next pointers are set to *NULL*.

Example 1:

![117_sample](https://assets.leetcode.com/uploads/2019/02/15/117_sample.png)

Input: root = [1,2,3,4,5,null,7]

Output: [1,#,2,3,#,4,5,7,#]

Explanation: Given the above binary tree (Figure A), your function should populate each next pointer to point to its next right node, just like in Figure B. The serialized output is in level order as connected by the next pointers, with '#' signifying the end of each level.

Example 2:

Input: root = []

Output: []

Constraints:

* The number of nodes in the tree is in the range [0, 6000].
* -100 <= Node.val <= 100

Follow-up:

* You may only use constant extra space.
* The recursive approach is fine. You may assume implicit stack space does not count as extra space for this problem.

#### Answer 15

```javascript
var connect = function(root) {
    //  JavaScript equivalent of a queue
    //      peek    --> fringe[0]
    //      deque   --> fringe[0] + fringe.shift()
    //      enque   --> fringe.push()
    //      isEmpty --> fringe.length == 0
    let fringe = [];
    fringe.push(root);
    fringe.push(null);
    
    while(fringe.length != 0) {
        let curr = fringe[0];
        fringe.shift();
        if(curr != null) {
            // get left child
            if(curr.left != null) fringe.push(curr.left);
                
            // get right child
            if(curr.right != null) fringe.push(curr.right);
            
            // set the pointer
            let peek = fringe[0];
            curr.next = peek;
            
            // we have ended the level and added all possible children on that level
            if(peek == null) {
                fringe.push(null);
            }
        }
    }
    
    return root;
};

//Your input
[1,2,3,4,5,null,7]
//Output
[1,#,2,3,#,4,5,7,#]
//Expected
[1,#,2,3,#,4,5,7,#]
```

### 572. Subtree of Another Tree

Given the roots of two binary trees *root* and *subRoot*, return *true* if there is a subtree of *root* with the same structure and node values of *subRoot* and *false* otherwise.

A subtree of a binary tree *tree* is a tree that consists of a node in *tree* and all of this node's descendants. The tree *tree* could also be considered as a subtree of itself.

Example 1:

![subtree1-tree](https://assets.leetcode.com/uploads/2021/04/28/subtree1-tree.jpg)

Input: root = [3,4,5,1,2], subRoot = [4,1,2]

Output: true

Example 2:

![subtree2-tree](https://assets.leetcode.com/uploads/2021/04/28/subtree2-tree.jpg)

Input: root = [3,4,5,1,2,null,null,null,null,0], subRoot = [4,1,2]

Output: false

Constraints:

* The number of nodes in the root tree is in the range [1, 2000].
* The number of nodes in the subRoot tree is in the range [1, 1000].
* -10^4 <= root.val <= 10^4
* -10^4 <= subRoot.val <= 10^4

#### Answer 16

```javascript
// DFS Version:
const isSubtree = (root, subRoot) => {
  const areEqual = (node1, node2) => {
    if (!node1 || !node2) return !node1 && !node2;
    if (node1.val !== node2.val) return false;
    return areEqual(node1.left, node2.left) && areEqual(node1.right, node2.right);
  }
  const dfs = (node) => {
    if (!node) return false;
    if (areEqual(node, subRoot)) return true;
    return dfs(node.left) || dfs(node.right);
  }
  return dfs(root);
};

//Your input
[3,4,5,1,2]
[4,1,2]
//Output
true
//Expected
true
```

### 1091. Shortest Path in Binary Matrix

Given an *n x n* binary matrix *grid*, return the length of the shortest *clear path* in the matrix. If there is no clear path, return *-1*.

A *clear path* in a binary matrix is a path from the *top-left* cell (i.e., *(0, 0)*) to the *bottom-right* cell (i.e., *(n - 1, n - 1)*) such that:

* All the visited cells of the path are *0*.
* All the adjacent cells of the path are *8-directionally* connected (i.e., they are different and they share an edge or a corner).

The *length of a clear path* is the number of visited cells of this path.

Example 1:

![example1_1](https://assets.leetcode.com/uploads/2021/02/18/example1_1.png)

Input: grid = [[0,1],[1,0]]

Output: 2

Example 2:

![example2_1](https://assets.leetcode.com/uploads/2021/02/18/example2_1.png)

Input: grid = [[0,0,0],[1,1,0],[1,1,0]]

Output: 4

Example 3:

Input: grid = [[1,0,0],[1,1,0],[1,1,0]]

Output: -1

Constraints:

* n == grid.length
* n == grid[i].length
* 1 <= n <= 100
* grid[i][j] is 0 or 1

#### Answer 17

```javascript
var shortestPathBinaryMatrix = function(grid) {
    
    /*
       Classic BFS with level traversal.
       Time:  O(m*n)
       Space: O(m*n)
    */
    
    
    // Edge cases
    //   empty grid
    if(grid.length == 0){
        return -1;
    }
    //   blocked starting point
    if(grid[0][0] == 1){
        return -1;
    }
    
    // 
    const m = grid.length;
    const n = grid[0].length;

    // moving directions
    const DIR = [
        // 
        [0,1],
        [0,-1],
        [1,0],
        [-1,0],
        // diagonals
        [1,1],
        [-1,1],
        [1,-1],
        [-1,-1],
    ];
    
    // define target
    const target = {row: m-1, col: n-1};
        
    // preventing double visits
    // could be replaced with changing original grid
    // by changing visited 0 cells to 1
    const _seen = new Set();
    const seen$ = (r, c) => _seen.has(r*n+c);
    const visit$ = (r, c) => {
        _seen.add(r*n+c);
        return {row: r, col: c};
    }
    
    const q = [visit$(0,0)];
    
    let path  = 0
    
    while(q.length>0){
        path++;    
        // level traversal: in our case level it is steps in the grid
        for(let i=q.length;i>0;i--){
            let {row, col} = q.shift();
            
            // if target found - return current step
            // since it is BFS the very first occurences will be
            // at the shortest path
            if(row == target.row && col == target.col){
                return path;
            }
            
            for(let d of DIR){
                
                let nr = row + d[0];
                let nc = col + d[1];
                
                // bounds check
                if(nr < 0 || nc < 0 || nr >=m || nc >= n){
                    continue;
                }
                
                // ignore visited
                if(seen$(nr, nc)){
                    continue;
                }
                
                // visit only empty cells
                if(grid[nr][nc] == 0){
                    q.push(visit$(nr, nc));
                }
            }
        }
    }
    
    // all possible ways have been checked and no target achieved
    return -1;
  
};

// Runtime: 108 ms, faster than 90.57% of JavaScript online submissions for Shortest Path in Binary Matrix.
var shortestPathBinaryMatrix = function(grid) {
    const n = grid.length
    if(grid[0][0] || grid[n-1][n-1]) return -1
    const queue = []
    const dist = 0
    queue.push([0, 0, dist+1])
    const directions = [[-1,-1],[-1,0],[-1,1],
                        [0,-1],[0,1],
                        [1,-1],[1,0],[1,1]]
        for(const [i, j, d] of queue){
            if(i === n-1 && j === n-1) return d
            for(const [x, y] of directions){
                const newI = i + x
                const newJ = j + y
                 if(0 <= newI && newI < n && 0 <= newJ && newJ < n && !grid[newI][newJ]){
                     queue.push([newI, newJ, d+1])
                     grid[newI][newJ] = 1
                 }
            }
        }
    return -1
};

//Your input
[[0,1],[1,0]]
//Output
2
//Expected
2
```

### 130. Surrounded Regions

Given an *m x n* matrix *board* containing *'X'* and *'O'*, capture all regions that are 4-directionally surrounded by *'X'*.

A region is *captured* by flipping all *'O'*s into *'X'*s in that surrounded region.

Example 1:

![xogrid](https://assets.leetcode.com/uploads/2021/02/19/xogrid.jpg)

Input: board = [["X","X","X","X"],["X","O","O","X"],["X","X","O","X"],["X","O","X","X"]]

Output: [["X","X","X","X"],["X","X","X","X"],["X","X","X","X"],["X","O","X","X"]]

Explanation: Surrounded regions should not be on the border, which means that any 'O' on the border of the board are not flipped to 'X'. Any 'O' that is not on the border and it is not connected to an 'O' on the border will be flipped to 'X'. Two cells are connected if they are adjacent cells connected horizontally or vertically.

Example 2:

Input: board = [["X"]]

Output: [["X"]]

Constraints:

* m == board.length
* n == board[i].length
* 1 <= m, n <= 200
* board[i][j] is 'X' or 'O'.

#### Answer 18

```javascript
var solve = function(board) {
    if(!board.length)return
    for(let i=0;i<board.length;i++){
        dfs(board,i,0)
        dfs(board,i,board[0].length-1)
    }
    for(let j=0;j<board[0].length;j++){
        dfs(board,0,j)
        dfs(board,board.length-1,j)
    }
    for(let i=0;i<board.length;i++){
        for(let j=0;j<board[0].length;j++){
            if(board[i][j] == 'O') board[i][j] = 'X'
            else if(board[i][j] == 'p') board[i][j] = 'O'
        }
    }
};

let dfs = (board,i,j)=>{
    if(i>=0 && j>=0 && i<board.length && j<board[0].length && board[i][j] === 'O'){
        board[i][j] = 'p'
        dfs(board,i+1,j)
        dfs(board,i,j+1)
        dfs(board,i-1,j)
        dfs(board,i,j-1)
    }
    return
};

//Your input
[["X","X","X","X"],["X","O","O","X"],["X","X","O","X"],["X","O","X","X"]]
//Output
[["X","X","X","X"],["X","X","X","X"],["X","X","X","X"],["X","O","X","X"]]
//Expected
[["X","X","X","X"],["X","X","X","X"],["X","X","X","X"],["X","O","X","X"]]
```

### 797. All Paths From Source to Target

Given a directed acyclic graph (*DAG*) of *n* nodes labeled from *0* to *n - 1*, find all possible paths from node 0 to node *n - 1* and return them in *any order*.

The graph is given as follows: *graph[i]* is a list of all nodes you can visit from node *i* (i.e., there is a directed edge from node *i* to node *graph[i][j]*).

Example 1:

![all_1](https://assets.leetcode.com/uploads/2020/09/28/all_1.jpg)

Input: graph = [[1,2],[3],[3],[]]

Output: [[0,1,3],[0,2,3]]

Explanation: There are two paths: 0 -> 1 -> 3 and 0 -> 2 -> 3.

Example 2:

![all_2](https://assets.leetcode.com/uploads/2020/09/28/all_2.jpg)

Input: graph = [[4,3,1],[3,2,4],[3],[4],[]]

Output: [[0,4],[0,3,4],[0,1,3,4],[0,1,2,3,4],[0,1,4]]

Example 3:

Input: graph = [[1],[]]

Output: [[0,1]]

Example 4:

Input: graph = [[1,2,3],[2],[3],[]]

Output: [[0,1,2,3],[0,2,3],[0,3]]

Example 5:

Input: graph = [[1,3],[2],[3],[]]

Output: [[0,1,2,3],[0,3]]

Constraints:

* n == graph.length
* 2 <= n <= 15
* 0 <= graph[i][j] < n
* graph[i][j] != i (i.e., there will be no self-loops).
* All the elements of graph[i] are *unique*.
* The input graph is *guaranteed* to be a *DAG*.

#### Answer 19

```javascript
var allPathsSourceTarget = function(graph) {
    const paths = []
    const dfs = (index, path) => {
// only if the path a target path
        if(path[path.length - 1] == graph.length - 1) {
            paths.push(path);
            return;
        }
        for(let i = 0; i < graph[index].length; i++) {
            dfs(graph[index][i], [...path, graph[index][i]])
        }
    }
    dfs(0, [0])
    return paths
};

//Your input
[[1,2],[3],[3],[]]
//Output
[[0,1,3],[0,2,3]]
//Expected
[[0,1,3],[0,2,3]]
```

## Recursion / Backtracking

### 78. Subsets

Given an integer array *nums* of *unique* elements, return all possible subsets (the power set).

The solution set *must not* contain duplicate subsets. Return the solution in *any order*.

Example 1:

Input: nums = [1,2,3]

Output: [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]

Example 2:

Input: nums = [0]

Output: [[],[0]]

Constraints:

* 1 <= nums.length <= 10
* -10 <= nums[i] <= 10
* All the numbers of nums are unique.

#### Answer 20

```javascript
var subsets = function(nums) {
    let answer =[];
    let ip = [nums];
    let op=[]
    FindSunsets(nums,op)
    function FindSunsets(ip,op){
        ip=[...ip]
      if(ip.length==0){
          answer.push(op)
          return
      }  
       let op1 = [...op];
       let op2 = [...op];
        op2.push(ip[0])
        ip.shift();
        FindSunsets(ip,op1)
        FindSunsets(ip,op2);
        return
    }
    return answer
};

//Your input
[1,2,3]
//Output
[[],[3],[2],[2,3],[1],[1,3],[1,2],[1,2,3]]
//Expected
[[],[3],[2],[2,3],[1],[1,3],[1,2],[1,2,3]]
```

### 90. Subsets II

Given an integer array *nums* that may contain duplicates, return all possible subsets (the power set).

The solution set must not contain duplicate subsets. Return the solution in *any order*.

Example 1:

Input: nums = [1,2,2]

Output: [[],[1],[1,2],[1,2,2],[2],[2,2]]

Example 2:

Input: nums = [0]

Output: [[],[0]]

Constraints:

* 1 <= nums.length <= 10
* -10 <= nums[i] <= 10

#### Answer 21

```javascript
const subsetsWithDup = function(nums) {
    //sort the array so that duplicates will be next to each other
    nums.sort();
    const result = [];
    result.push([]);
    let pointer1 = 0,
        pointer2 = 0;
    for (let i = 0; i < nums.length; i++) {
        pointer1 = 0;
        
        if (i > 0 && nums[i] === nums[i - 1]) {
            pointer1 = pointer2 + 1;
        }
        pointer2 = result.length - 1;
        for (let j = pointer1; j < pointer2 + 1; j++) {
            const set = result[j].slice(0);
            set.push(nums[i]);
            result.push(set);
        }
    }
    return result;
};

//Your input
[1,2,2]
//Output
[[],[1],[2],[1,2],[2,2],[1,2,2]]
//Expected
[[],[1],[2],[1,2],[2,2],[1,2,2]]
```

### 47. Permutations II

Given a collection of numbers, *nums*, that might contain duplicates, return all possible unique permutations in *any order*.

Example 1:

Input: nums = [1,1,2]

Output: [[1,1,2],[1,2,1],[2,1,1]]

Example 2:

Input: nums = [1,2,3]

Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]

Constraints:

* 1 <= nums.length <= 8
* -10 <= nums[i] <= 10
