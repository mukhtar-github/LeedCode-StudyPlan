# Algorithm

## Binary Search

### 704. Binary Search

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

#### Answer 1

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

### 278. First Bad Version

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

#### Answer 2

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

Your input
5
4
Output
4
Expected
4
```

### 35. Search Insert Position

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

#### Answer 3

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

Your input
[1,3,5,6]
5
Output
2
Expected
2
```

## Two Pointers

### 977. Squares of a Sorted Array

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

#### Answer 4

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

### 189. Rotate Array

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

#### Answer 5

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

### 283. Move Zeroes

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

#### Answer 6

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

### 167. Two Sum II - Input array is sorted

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

#### Answer 7

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

### 344. Reverse String

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

#### Answer 8

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

### 557. Reverse Words in a String III

Given a string *s*, reverse the order of characters in each word within a sentence while still preserving whitespace and initial word order.

Example 1:

Input: s = "Let's take LeetCode contest"

Output: "s'teL ekat edoCteeL tsetnoc"

Example 2:

Input: s = "God Ding"

Output: "doG gniD"

Constraints:

1 <= s.length <= 5 * 10^4

s contains printable ASCII characters.

s does not contain any leading or trailing spaces.

There is at least one word in s.

All the words in s are separated by a single space.

#### Answer 9

```javascript
var reverseWords = function(s) {
    return s.split(" ").map(word=> word.split("").reverse().join("")).join(" ")
};

Your input
"Let's take LeetCode contest"
Output
"s'teL ekat edoCteeL tsetnoc"
Expected
"s'teL ekat edoCteeL tsetnoc"
```

### 876. Middle of the Linked List

Given the *head* of a singly linked list, return the middle node of the linked list. If there are two middle nodes, return **the second middle** node.

Example 1:

![lc-midlist1](https://assets.leetcode.com/uploads/2021/07/23/lc-midlist1.jpg)

Input: head = [1,2,3,4,5]

Output: [3,4,5]

Explanation: The middle node of the list is node 3.

Example 2:

![lc-midlist2](https://assets.leetcode.com/uploads/2021/07/23/lc-midlist2.jpg)

Input: head = [1,2,3,4,5,6]

Output: [4,5,6]

Explanation: Since the list has two middle nodes with values 3 and 4, we return the second one.

Constraints:

* The number of nodes in the list is in the range [1, 100].
* 1 <= Node.val <= 100

#### Answer 10

```javascript
var middleNode = function(head) {

    let len = 0;
    let current = head;
    
    while(current) {
        len++;
        current = current.next;
    }
    
    let mid = Math.floor(len/2);
    
    while(mid){
        head = head.next;
        mid--;
    }
    
    return head;
};

Your input
[1,2,3,4,5]
Output
[3,4,5]
Expected
[3,4,5]

var middleNode = function(head) {
    slow = fast = head;
    while (fast && fast.next) {
        slow = slow.next;
        fast = fast.next.next;
    }
    return slow;
};

var middleNode = function(head) {
    let A = [head];
    while (A[A.length - 1].next != null)
        A.push(A[A.length - 1].next);
    return A[Math.trunc(A.length / 2)];
};
```

### 19. Remove Nth Node From End of List

Given the *head* of a linked list, remove the *nth* node from the end of the list and return its head.

Example 1:

![remove_ex1](https://assets.leetcode.com/uploads/2020/10/03/remove_ex1.jpg)

Input: head = [1,2,3,4,5], n = 2

Output: [1,2,3,5]

Example 2:

Input: head = [1], n = 1

Output: [ ]

Example 3:

Input: head = [1,2], n = 1

Output: [1]

Constraints:

* The number of nodes in the list is sz.
* 1 <= sz <= 30
* 0 <= Node.val <= 100
* 1 <= n <= sz

**Follow up**: Could you do this in one pass?

#### Answer 11

```javascript
var removeNthFromEnd = function(head, n) { 
    let dummy = new ListNode(0, head);
    let prev = dummy;
    let node = head;
    let count = 1;
    while (node.next) {
        if (count === n) {
            prev = prev.next;
        } else {
            count++;
        }
        node = node.next;
    }
    prev.next = prev.next.next;
    return dummy.next;
};

Your input
[1,2,3,4,5]
2
Output
[1,2,3,5]
Expected
[1,2,3,5]

var removeNthFromEnd = function(head, n) {
    let fast = head, slow = head
    for (let i = 0; i < n; i++) fast = fast.next
    if (!fast) return head.next
    while (fast.next) fast = fast.next, slow = slow.next
    slow.next = slow.next.next
    return head
};
```

## Sliding Window

### 3. Longest Substring Without Repeating Characters

Given a string *s*, find the length of the longest substring without repeating characters.

Example 1:

Input: s = "abcabcbb"

Output: 3

Explanation: The answer is "abc", with the length of 3.

Example 2:

Input: s = "bbbbb"

Output: 1

Explanation: The answer is "b", with the length of 1.

Example 3:

Input: s = "pwwkew"

Output: 3

Explanation: The answer is "wke", with the length of 3. Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.

Example 4:

Input: s = ""

Output: 0

Constraints:

0 <= s.length <= 5 * 10^4

s consists of English letters, digits, symbols and spaces.

#### Answer 12

```javascript
var lengthOfLongestSubstring = function (s) {
    const hashMap = new Map();
    let maxLength = 0;
    let left = 0;
    for (let right = 0; right < s.length; right++) {
        if (hashMap.get(s[right])) {
            left = Math.max(hashMap.get(s[right]), left);
        }
        maxLength = Math.max(maxLength, right - left + 1);
        hashMap.set(s[right], right + 1);
    }
    return maxLength;
};

Your input
"abcabcbb"
Output
3
Expected
3
```

### 567. Permutation in String

Given two strings *s1* and *s2*, return *true* if *s2* contains a permutation of *s1*, or *false* otherwise.

In other words, return *true* if one of *s1*'s permutations is the substring of *s2*.

Example 1:

Input: s1 = "ab", s2 = "eidbaooo"

Output: true

Explanation: s2 contains one permutation of s1 ("ba").

Example 2:

Input: s1 = "ab", s2 = "eidboaoo"

Output: false

Constraints:

1 <= s1.length, s2.length <= 10^4

s1 and s2 consist of lowercase English letters.

#### Answer 13

```javascript
var checkInclusion = function(s1, s2) {
    if (s1 === "" || s2 === "") {
        return false;
    }
    let m = new Map();
    // Record every character of s1 to Hash table with entry being
    // (character, number of occurrences)
    for (let i = 0; i < s1.length; i++) {
        m.set(s1[i], m.get(s1[i]) + 1 || 1);
    }
    let start = 0, windowSize = s1.length;
    // number of unique characters to collect
    let counter = m.size;
    for (let end = 0; end < s2.length; end++) {
        let char = s2[end];
        if (m.has(char)) m.set(char, m.get(char) - 1);
        if (m.get(char) === 0) counter--; // we collected all occurrences of this char
        // we collected all occurrences of every character in s1
        while (counter === 0) {
            if (end-start+1 === windowSize) return true;
            if (m.has(s2[start])) m.set(s2[start], m.get(s2[start]) + 1);
            if (m.get(s2[start]) === 1) counter++; // we should collect one more unique char
            start++;
        }
    }
    return false;
    // T.C: O(M+N), M = length of s1, N = length of s2
    // S.C: O(M)
};


Your input
"ab"
"eidbaooo"
Output
true
Expected
true
```

## Breadth-First Search / Depth-First Search

### 733. Flood Fill

An image is represented by an *m x n* integer grid *image* where *image[i][j]* represents the pixel value of the image.

You are also given three integers *sr, sc*, and *newColor*. You should perform a **flood fill** on the image starting from the pixel *image[sr][sc]*.

To perform a **flood fill**, consider the starting pixel, plus any pixels connected **4-directionally** to the starting pixel of the same color as the starting pixel, plus any pixels connected **4-directionally** to those pixels (also with the same color), and so on. Replace the color of all of the aforementioned pixels with *newColor*.

Return the modified image after performing the flood fill.

Example 1

![flood1-grid.jpg](https://assets.leetcode.com/uploads/2021/06/01/flood1-grid.jpg)

**Input**: image = [[1,1,1],[1,1,0],[1,0,1]], sr = 1, sc = 1, newColor = 2

**Output**: [[2,2,2],[2,2,0],[2,0,1]]

**Explanation**: From the center of the image with position (sr, sc) = (1, 1) (i.e., the red pixel), all pixels connected by a path of the same color as the starting pixel (i.e., the blue pixels) are colored with the new color.

Note the bottom corner is not colored 2, because it is not 4-directionally connected to the starting pixel.

Example 2

**Input**: image = [[0,0,0],[0,0,0]], sr = 0, sc = 0, newColor = 2

**Output**: [[2,2,2],[2,2,2]]

Constraints

* m == image.length
* n == image[i].length
* 1 <= m, n <= 50
* 0 <= image[i][j], newColor < 2^16
* 0 <= sr < m
* 0 <= sc < n

#### Answer 14

```javascript
var floodFill = function(image, sr, sc, newColor) {
    let startingPixel = image[sr][sc]
    const dfs = (image, sr, sc, newColor) => {
        if (sr < 0 || sc < 0 ||  sr >= image.length || sc >= image[0].length || image[sr][sc] !== startingPixel || image[sr][sc] === newColor) return;
        image[sr][sc] = newColor

        dfs(image, sr - 1, sc, newColor);
        dfs(image, sr + 1, sc, newColor);
        dfs(image, sr, sc - 1, newColor);
        dfs(image, sr, sc + 1, newColor);
    }
    dfs(image, sr, sc, newColor);
    return image
};


Your input
[[1,1,1],[1,1,0],[1,0,1]]
1
1
2
Output
[[2,2,2],[2,2,0],[2,0,1]]
Expected
[[2,2,2],[2,2,0],[2,0,1]]
```

### 695. Max Area of Island

You are given an *m x n* binary matrix *grid*. An island is a group of *1*'s (representing land) connected **4-directionally** (horizontal or vertical.) You may assume all four edges of the grid are surrounded by water.

The **area** of an island is the number of cells with a value *1* in the island.

Return the maximum **area** of an island in *grid*. If there is no island, return *0*.

Example 1:

![maxarea1-grid](https://assets.leetcode.com/uploads/2021/05/01/maxarea1-grid.jpg)

**Input**: grid = [[0,0,1,0,0,0,0,1,0,0,0,0,0],
[0,0,0,0,0,0,0,1,1,1,0,0,0],[0,1,1,0,1,0,0,0,0,0,0,0,0],
[0,1,0,0,1,1,0,0,1,0,1,0,0],[0,1,0,0,1,1,0,0,1,1,1,0,0],
[0,0,0,0,0,0,0,0,0,0,1,0,0],[0,0,0,0,0,0,0,1,1,1,0,0,0],
[0,0,0,0,0,0,0,1,1,0,0,0,0]]

**Output**: 6

**Explanation**: The answer is not 11, because the island must be connected 4-directionally.

Example 2:

**Input**: grid = [[0,0,0,0,0,0,0,0]]

**Output**: 0

**Constraints**:

* m == grid.length
* n == grid[i].length
* 1 <= m, n <= 50
* grid[i][j] is either 0 or 1.

#### Answer 15

```javascript
var maxAreaOfIsland = function(grid) {
  const dfs = (x, y) => {
    if (x < 0 || y < 0 || x >= grid.length || y >= grid[0].length || grid[x][y] === 0) return 0;
    grid[x][y] = 0;
    return 1 + dfs(x-1, y) + dfs(x , y+1) + dfs(x+1, y) + dfs(x, y-1);
  }
  
  let max = 0;
  for (let x = 0; x < grid.length; x++) {
    for (let y = 0; y < grid[0].length; y++) {
      max = Math.max(max, dfs(x, y));
    }
  }
  
  return max;
};

Your input
[[0,0,1,0,0,0,0,1,0,0,0,0,0],[0,0,0,0,0,0,0,1,1,1,0,0,0],
[0,1,1,0,1,0,0,0,0,0,0,0,0],[0,1,0,0,1,1,0,0,1,0,1,0,0],
[0,1,0,0,1,1,0,0,1,1,1,0,0],[0,0,0,0,0,0,0,0,0,0,1,0,0],
[0,0,0,0,0,0,0,1,1,1,0,0,0],[0,0,0,0,0,0,0,1,1,0,0,0,0]]
Output
6
Expected
6
```

### 617. Merge Two Binary Trees

You are given two binary trees *root1* and *root2*.

Imagine that when you put one of them to cover the other, some nodes of the two trees are overlapped while the others are not. You need to merge the two trees into a new binary tree. The merge rule is that if two nodes overlap, then sum node values up as the new value of the merged node. Otherwise, the NOT null node will be used as the node of the new tree.

*Return the merged tree*.

**Note**: The merging process must start from the root nodes of both trees.

Example 1:

![merge](https://assets.leetcode.com/uploads/2021/02/05/merge.jpg)

Input: root1 = [1,3,2,5], root2 = [2,1,3,null,4,null,7]

Output: [3,4,5,5,4,null,7]

Example 2:

Input: root1 = [1], root2 = [1,2]

Output: [2,2]

Constraints:

The number of nodes in both trees is in the range [0, 2000].

-10^4 <= Node.val <= 10^4

#### Answer 16

```javascript
const mergeTrees = (t1, t2) => {
    if (!t1 && !t2) return null;
    
    const left = mergeTrees(t1 && t1.left, t2 && t2.left);
    const right = mergeTrees(t1 && t1.right, t2 && t2.right);
        
    return new TreeNode(
        (t1 && t1.val) + (t2 && t2.val),
        left,
        right,
    );
};

Your input
[1,3,2,5]
[2,1,3,null,4,null,7]
Output
[3,4,5,5,4,null,7]
Expected
[3,4,5,5,4,null,7]
```

### 116. Populating Next Right Pointers in Each Node

You are given a **perfect binary tree** where all leaves are on the same level, and every parent has two children. The binary tree has the following definition:

```javascript
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

![116_sample](https://assets.leetcode.com/uploads/2019/02/14/116_sample.png)

Input: root = [1,2,3,4,5,6,7]

Output: [1,#,2,3,#,4,5,6,7,#]

Explanation: Given the above perfect binary tree (Figure A), your function should populate each next pointer to point to its next right node, just like in Figure B. The serialized output is in level order as connected by the next pointers, with '#' signifying the end of each level.

Example 2:

Input: root = []

Output: []

Constraints:

* The number of nodes in the tree is in the range *[0, 212 - 1]*.
* -1000 <= Node.val <= 1000

Follow-up:

* You may only use constant extra space.
* The recursive approach is fine. You may assume implicit stack space does not count as extra space for this problem.

#### Answer 17

```javascript
var connect = function(curr) {
    if (curr == null)
        return curr;
    var root = curr;
    var temp = null;
    while (root.left != null) {
        temp = root;
        while (temp != null) {
            temp.left.next = temp.right;
            if (temp.next != null)
                temp.right.next = temp.next.left;
            temp = temp.next;
        }
        root = root.left;
    }
    return curr;
};

Your input
[1,2,3,4,5,6,7]
Output
[1,#,2,3,#,4,5,6,7,#]
Expected
[1,#,2,3,#,4,5,6,7,#]
```

### 542. 01 Matrix

Given an *m x n* binary matrix *mat*, return the distance of the nearest *0* for each cell.

The distance between two adjacent cells is *1*.

Example 1:

![01-1-grid](https://assets.leetcode.com/uploads/2021/04/24/01-1-grid.jpg)

Input: mat = [[0,0,0],[0,1,0],[0,0,0]]

Output: [[0,0,0],[0,1,0],[0,0,0]]

Example 2:

![01-2-grid](https://assets.leetcode.com/uploads/2021/04/24/01-2-grid.jpg)

Input: mat = [[0,0,0],[0,1,0],[1,1,1]]

Output: [[0,0,0],[0,1,0],[1,2,1]]

Constraints:

* m == mat.length
* n == mat[i].length
* 1 <= m, n <= 104
* 1 <= m * n <= 104
* mat[i][j] is either 0 or 1.
* There is at least one 0 in mat.

#### Answer 18

```javascript
var updateMatrix = function(mat) {
    let rows = mat.length;
    let columns = mat[0].length;
    // console.log("rows", rows, "columns", columns)
    // scan from top left to bottom right
    const scanMatrixFromTopLeft = (mat) => {
        for(let g=0; g<rows; g++){
             for(let k=0; k<columns; k++){
                 if( mat[g][k] > 0 ) {
                     mat[g][k] = Infinity; // becasue at this time we do not know what is the minimum dist so a maximum value
                    if( g > 0 )
                        mat[g][k] = Math.min( 
                                        mat[g][k], mat[g-1][k] + 1);
                     if( k > 0 )
                        mat[g][k] = Math.min( 
                                        mat[g][k], mat[g][k-1] + 1
                                       ) 
                                    ;   
                    // console.log("g, k", g, k, "&&&&", mat[g][k])             
                 }
             }
        }
    }
    
    const scanMatrixFromBottomRight = (mat) => {
        for(let g=(rows-1); g>=0; g--){
             for(let k=(columns-1); k>=0; k--){
                 if( mat[g][k] > 0 ) {
                    if( (g+1) < rows )
                        mat[g][k] = Math.min( 
                                        mat[g][k], mat[g+1][k] + 1);
                     if( (k+1) < columns )
                        mat[g][k] = Math.min( 
                                        mat[g][k], mat[g][k+1] + 1
                                       ) 
                                      
                 }
             }
        }
    }
    
    scanMatrixFromTopLeft(mat);
    scanMatrixFromBottomRight(mat);
    return mat; 
};

Your input
[[0,0,0],[0,1,0],[0,0,0]]
Output
[[0,0,0],[0,1,0],[0,0,0]]
Expected
[[0,0,0],[0,1,0],[0,0,0]]
```

### 994. Rotting Oranges

You are given an *m x n* grid where each cell can have one of three values:

* 0 representing an empty cell,
* 1 representing a fresh orange, or
* 2 representing a rotten orange.

Every minute, any fresh orange that is **4-directionally** adjacent to a rotten orange becomes rotten.

*Return the minimum number of minutes that must elapse until no cell has a fresh orange. If this is impossible, return -1*.

Example 1:

![oranges](https://assets.leetcode.com/uploads/2019/02/16/oranges.png)

Input: grid = [[2,1,1],[1,1,0],[0,1,1]]

Output: 4

Example 2:

Input: grid = [[2,1,1],[0,1,1],[1,0,1]]

Output: -1

Explanation: The orange in the bottom left corner (row 2, column 0) is never rotten, because rotting only happens 4-directionally.

Example 3:

Input: grid = [[0,2]]

Output: 0

Explanation: Since there are already no fresh oranges at minute 0, the answer is just 0.

Constraints:

* m == grid.length
* n == grid[i].length
* 1 <= m, n <= 10
* grid[i][j] is 0, 1, or 2.

#### Answer 19

```javascript
/**
 * @param {number[][]} grid
 * @return {number}
 */
var orangesRotting = function(grid) {
    let x = 2, runAgain = true, hasOne = false;

const markRotten = (grid,i,j,x) => {
    grid[i+1] && grid[i+1][j] === 1 && (grid[i+1][j] = x+1);
    grid[i][j+1] === 1 && (grid[i][j+1] = x+1);
    grid[i-1] && grid[i-1][j] === 1 && (grid[i-1][j] = x+1);
    grid[i][j-1] === 1 && (grid[i][j-1] = x+1);
}

while(runAgain) {
    runAgain = hasOne = false;
    for(let i =0;i< grid.length;i++){
        for(let j=0;j< grid[0].length;j++){
            if(grid[i][j] === x){
                runAgain = true;
                markRotten(grid,i,j,x);
            } 
            grid[i][j] === 1 && (hasOne=true);
        }
    }
    x++;
}

return hasOne ? -1 : x<4 ? 0 : x-4;
};

Your input
[[2,1,1],[1,1,0],[0,1,1]]
Output
4
Expected
4
```

## Recursion / Backtracking

### 21. Merge Two Sorted Lists

Merge two sorted linked lists and return it as a **sorted** list. The list should be made by splicing together the nodes of the first two lists.

Example 1:

![merge_ex1](https://assets.leetcode.com/uploads/2020/10/03/merge_ex1.jpg)

Input: l1 = [1,2,4], l2 = [1,3,4]

Output: [1,1,2,3,4,4]

Example 2:

Input: l1 = [], l2 = []

Output: []

Example 3:

Input: l1 = [], l2 = [0]

Output: [0]

Constraints:

* The number of nodes in both lists is in the range [0, 50].
* -100 <= Node.val <= 100
* Both l1 and l2 are sorted in non-decreasing order.

#### Answer 20

```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */    
var mergeTwoLists = function(l1, l2) {
    let tempNode = new ListNode(0, null);
    let currentNode = tempNode;
    
    while (l1 && l2) {
        if(l1.val < l2.val) {
            currentNode.next = l1;
            l1 = l1.next
        } else {
            currentNode.next = l2;
            l2 = l2.next
        }
        currentNode = currentNode.next;
    }
    currentNode.next = l1 || l2;
    
    return tempNode.next;
};

Your input
[1,2,4]
[1,3,4]
Output
[1,1,2,3,4,4]
Expected
[1,1,2,3,4,4]
```

### 206. Reverse Linked List

Given the *head* of a singly linked list, reverse the list, and return the *reversed list*.

Example 1:

![rev1ex1](https://assets.leetcode.com/uploads/2021/02/19/rev1ex1.jpg)

Input: head = [1,2,3,4,5]

Output: [5,4,3,2,1]

Example 2:

![rev1ex2](https://assets.leetcode.com/uploads/2021/02/19/rev1ex2.jpg)

Input: head = [1,2]

Output: [2,1]

Example 3:

Input: head = []

Output: []

Constraints:

* The number of nodes in the list is the range [0, 5000].
* -5000 <= Node.val <= 5000

Follow up: A linked list can be reversed either iteratively or recursively. Could you implement both?

#### Answer 21

```javascript
var reverseList = function(head) {
    let [prev, cur] = [null, head]
    while(cur) {
        [cur.next, prev, cur] = [prev, cur, cur.next]
    }
    return prev
}

Your input
[1,2,3,4,5]
Output
[[5,4,3,2,1]
Expected
[5,4,3,2,1]
```

### 77. Combinations

Given two integers *n* and *k*, return all possible combinations of *k* numbers out of the range *[1, n]*.

You may return the answer in **any order**.

Example 1:

Input: n = 4, k = 2

Output:
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]

Example 2:

Input: n = 1, k = 1

Output: [[1]]

Constraints:

* 1 <= n <= 20
* 1 <= k <= n

#### Answer 22

```javascript
/**
 * @param {number} n
 * @param {number} k
 * @return {number[][]}
 */

var combine = function(n, k) {
    let ans = []
    backtracking(ans,[],1,n,k)
    return ans
};
var backtracking = function(ans,tmp,start,n,k) {
    if(tmp.length == k){
      ans.push(Array.from(tmp))
      return
    }
    for(let i=start;i<=n;++i){
      tmp.push(i)
      backtracking(ans,tmp,i+1,n,k)
      tmp.pop()
    }
};

var combine = function(n, k) {
    if (n === 1) {
        return [[1]];
    }
    let result = [];
    combineHelper(n, k, 1, [], result);
    return result;
};

var combineHelper = function(n, k, startIdx, currentCombo, result) {
    if (currentCombo.length && currentCombo.length === k) {
        result.push(currentCombo.slice());
        return;
    }
    for (let i = startIdx; i <= n; i++) {
        currentCombo.push(i);
        combineHelper(n, k, i + 1, currentCombo, result);
        currentCombo.pop();
    } 
};

Your input
4
2
Output
[[1,2],[1,3],[1,4],[2,3],[2,4],[3,4]]
Expected
[[1,2],[1,3],[1,4],[2,3],[2,4],[3,4]]
```

### 46. Permutations

Given an array *nums* of distinct integers, return all the possible permutations. You can return the answer in **any order**.

Example 1:

Input: nums = [1,2,3]

Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]

Example 2:

Input: nums = [0,1]

Output: [[0,1],[1,0]]

Example 3:

Input: nums = [1]

Output: [[1]]

Constraints:

* 1 <= nums.length <= 6
* -10 <= nums[i] <= 10
* All the integers of nums are *unique*.

#### Answer 23

```javascript
var permute = function(nums) {
    let temp = []
    let result = []

    function backtracking(temp, nums) {
      if(nums.length == 0) {
          result.push([...temp])
          return
       }
    
      for(let i=0; i<nums.length; i++) {
          temp.push(nums[i])
          nums.splice(i, 1)
          backtracking(temp, nums)
          nums.splice(i, 0, temp.pop())
       }
    }
    backtracking(temp, nums)
    return result
};

Your input
[1,2,3]
Output
[[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
Expected
[[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```

### 784. Letter Case Permutation

Given a string *s*, we can transform every letter individually to be lowercase or uppercase to create another string.

Return a list of all possible strings we could create. You can return the output in **any order**.

Example 1:

Input: s = "a1b2"

Output: ["a1b2","a1B2","A1b2","A1B2"]

Example 2:

Input: s = "3z4"

Output: ["3z4","3Z4"]

Example 3:

Input: s = "12345"

Output: ["12345"]

Example 4:

Input: s = "0"

Output: ["0"]

Constraints:

* s will be a string with length between 1 and 12.
* s will consist only of letters or digits.

#### Answer 24

```javascript
var letterCasePermutation = function(S) {
    let n = S.length;
    let res = []
    let char = /[a-zA-Z]/
    let arr = []
    
    function backtrack(i){
        if(i == n){
            res.push(arr.join(''))
            return
        }
        
        if(char.test(S[i])){
            arr[i] = S[i].toLowerCase()
            backtrack(i+1)
            arr[i] = S[i].toUpperCase()
            backtrack(i+1)
        } else {
            arr[i] = S[i]
            backtrack(i+1)
        }
    }
    
    backtrack(0)
    return res
};

Your input
"a1b2"
Output
["a1b2","a1B2","A1b2","A1B2"]
Expected
["a1b2","a1B2","A1b2","A1B2"]
```

## Dynamic Programming

### 70. Climbing Stairs

You are climbing a staircase. It takes *n* steps to reach the top.

Each time you can either climb *1 or 2* steps. In how many distinct ways can you climb to the top?

Example 1:

Input: n = 2

Output: 2

Explanation: There are two ways to climb to the top.

1. 1 step + 1 step
2. 2 steps

Example 2:

Input: n = 3

Output: 3

Explanation: There are three ways to climb to the top.

1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step

Constraints:

* 1 <= n <= 45

#### Answer 25

#### Dynamic programming O(n) time and O(n) space

* O(n) time and space
* faster than memoization because we pre-allocate the array upfront

```javascript
var climbStairs = function(n) {
    const dp = new Array(n).fill(0);
    // Base Cases
    dp[0] = 0;
    dp[1] = 1;
    dp[2] = 2;

    // Sum the last 2 results behind me to get the current result.
    // dp[i] = dp[i-1] + dp[i-2]
    for(let i=3; i <= n; i++){
        dp[i] = dp[i-1] + dp[i-2]
    }
    return dp[n];
};

Your input
2
Output
2
Expected
2
```

### 198. House Robber

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security systems connected and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given an integer array *nums* representing the amount of money of each house, return the maximum amount of money you can rob tonight **without alerting the police**.

Example 1:

Input: nums = [1,2,3,1]

Output: 4

Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).

Total amount you can rob = 1 + 3 = 4.

Example 2:

Input: nums = [2,7,9,3,1]

Output: 12

Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).

Total amount you can rob = 2 + 9 + 1 = 12.

Constraints:

* 1 <= nums.length <= 100
* 0 <= nums[i] <= 400

#### Answer 26

```javascript
var rob = function(nums) {
    let prev1 = prev2 = 0;
    for(let i=0;i<nums.length;i++) {
        let tmp = prev1;
        prev1 = Math.max(prev2 + nums[i], prev1);
        prev2 = tmp;
    }
    return prev1;

};

Your input
[1,2,3,1]
Output
4
Expected
4
```

### 120. Triangle

Given a *triangle array, return the minimum path sum from top to bottom*.

For each step, you may move to an adjacent number of the row below. More formally, if you are on index *i* on the current row, you may move to either index *i* or index *i + 1* on the next row.

Example 1:

Input: triangle = [[2],[3,4],[6,5,7],[4,1,8,3]]

Output: 11

Explanation: The triangle looks like:

   2

  3 4

 6 5 7

4 1 8 3

The minimum path sum from top to bottom is 2 + 3 + 5 + 1 = 11 (underlined above).

Example 2:

Input: triangle = [[-10]]

Output: -10

Constraints:

* 1 <= triangle.length <= 200
* triangle[0].length == 1
* triangle[i].length == triangle[i - 1].length + 1
* -10^4 <= triangle[i][j] <= 10^4

#### Answer 27

```javascript
var minimumTotal = function(triangle) {
    for (let i = triangle.length-2; i >= 0; i--)
        for (let j = 0; j < triangle[i].length; j++)
            triangle[i][j] += Math.min(triangle[i+1][j], triangle[i+1][j+1])
    return triangle[0][0]
};

var minimumTotal = function(triangle) {
    for (var i = triangle.length-2;i>=0;i--){
        var prev_floor = triangle[i];
        var next_floor = triangle[i+1];
        for (var j = 0;j<prev_floor.length;j++){
            if (next_floor[j] > next_floor[j+1]){
                prev_floor[j] = prev_floor[j]+next_floor[j+1];
            }else{
                prev_floor[j] = prev_floor[j]+next_floor[j];
            }
        }
    }
    return triangle[0][0];
};

Your input
[[2],[3,4],[6,5,7],[4,1,8,3]]
Output
11
Expected
11
```
