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

You are given an array *prices* where *prices[i]* is the price of a given stock on the *i^th* day.

You want to maximize your profit by choosing a *single day* to buy one stock and choosing a *different day in the future* to sell that stock.

Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return *0*.

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
/*
steps:
1. Set minimum to first price
2. Keep calculating different until ith price is less than minimum
3. Maintain max diff and current diff
*/

var maxProfit = function(prices) {
    let min = prices[0];
    let diffCurrent = 0;
    let diffMax = 0;
    
    for (let i = 1; i < prices.length; i++) {
        if (prices[i] >= min) {
            // current price is greater than or equal to minumum so far
            // calculate diffCurrent and diffMax
            
            diffCurrent = prices[i] - min;
            
            if (diffCurrent > diffMax) {
                diffMax = diffCurrent;
            }
        } else {
            // current price is less than previous minimum
            // reset diffCurrent and minimum
            
            diffCurrent = 0;
            min = prices[i];
        }
    }
    
    return diffMax;
};

//Your input
[7,1,5,3,6,4]
//Output
5
//Expected
5
```

### 566. Reshape the Matrix

In MATLAB, there is a handy function called reshape which can reshape an m x n matrix into a new one with a different size r x c keeping its original data.

You are given an m x n matrix mat and two integers r and c representing the number of rows and the number of columns of the wanted reshaped matrix.

The reshaped matrix should be filled with all the elements of the original matrix in the same row-traversing order as they were.

If the reshape operation with given parameters is possible and legal, output the new reshaped matrix; Otherwise, output the original matrix.

Example 1:

![reshape1-grid](https://assets.leetcode.com/uploads/2021/04/24/reshape1-grid.jpg)

Input: mat = [[1,2],[3,4]], r = 1, c = 4

Output: [[1,2,3,4]]

Example 2:

![reshape2-grid](https://assets.leetcode.com/uploads/2021/04/24/reshape2-grid.jpg)

Input: mat = [[1,2],[3,4]], r = 2, c = 4

Output: [[1,2],[3,4]]

Constraints:

* m == mat.length
* n == mat[i].length
* 1 <= m, n <= 100
* -1000 <= mat[i][j] <= 1000
* 1 <= r, c <= 300

#### Answer 7

```javascript
var matrixReshape = function(mat, r, c) {
    const flat = mat.flat()
    if (flat.length !== r*c) return mat;
    return [...Array(r)].map(() => flat.splice(0,c)) 
};

var matrixReshape = function(mat, r, c) {
  if (mat.length * mat[0].length / r !== c || mat.length === r) return mat;
  const flat = mat.flat();
  while (r-- !== 0) flat.unshift(flat.splice(-c));
  return flat;
};

//Your input
[[1,2],[3,4]]
1
4
//Output
[[1,2,3,4]]
//Expected
[[1,2,3,4]]
```

### 118. Pascal's Triangle

Given an integer *numRows*, return the first *numRows* of *Pascal's triangle*.

In *Pascal's triangle*, each number is the sum of the two numbers directly above it as shown:

![PascalTriangleAnimated2](https://upload.wikimedia.org/wikipedia/commons/0/0d/PascalTriangleAnimated2.gif)

Example 1:

Input: numRows = 5

Output: [[1],[1,1],[1,2,1],[1,3,3,1],[1,4,6,4,1]]

Example 2:

Input: numRows = 1
Output: [[1]]

Constraints:

* 1 <= numRows <= 30

#### Answer 8

```javascript
var generate = function(numRows) {
    const res = [];
    let prevRow;
    
    for (let i = 1; i <= numRows; i++) {
        const row = new Array(i).fill(1);

        if (prevRow) {
            for (let j = 1; j < prevRow.length; j++) {
                const cs = prevRow[j] + prevRow[j - 1];
                row[j] = cs;
            }
        }
        
        res.push(row);
        prevRow = row;
    }
    
    return res;
};

/*
Idea:
For this problem, we can do pretty much just as the instructions tell us. We'll iterate through the building of Pascal's triangle (ans), row by row. When we create each new row, we should initially fill it with 1s so that we don't have to worry about the logic of filling the edge cells that only have one number above.

Then we can start on j = 1 for each row and repeat the process of summing up the value of the current cell until we reach the midpoint (mid). Since the triangle is symmetrical, we can actually fill both halves of the row at once, while we work inward.

Once we reach the end of the last row, we can return ans.

Time Complexity: O(N) where N is the numRowsth triangular number
Space Complexity: O(1)
*/

var generate = function(numRows) {
    let ans = new Array(numRows)
    for (let i = 0; i < numRows; i++) {
        let row = new Uint32Array(i+1).fill(1),
            mid = i >> 1
        for (let j = 1; j <= mid; j++) {
            let val = ans[i-1][j-1] + ans[i-1][j]
            row[j] = val, row[row.length-j-1] = val
        }
        ans[i] = row
    }
    return ans
};

//Your input
5
//Output
[[1],[1,1],[1,2,1],[1,3,3,1],[1,4,6,4,1]]
//Expected
[[1],[1,1],[1,2,1],[1,3,3,1],[1,4,6,4,1]]
```

### 36. Valid Sudoku

Determine if a *9 x 9* Sudoku board is valid. Only the filled cells need to be validated *according to the following rules*:

1. Each row must contain the digits *1-9* without repetition.
2. Each column must contain the digits *1-9* without repetition.
3. Each of the nine *3 x 3* sub-boxes of the grid must contain the digits *1-9* without repetition.

Note:

* A Sudoku board (partially filled) could be valid but is not necessarily solvable.
* Only the filled cells need to be validated according to the mentioned rules.

Example 1:

![250px-Sudoku-by-L2G-20050714.svg](https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)

Input: board =

[["5","3",".",".","7",".",".",".","."],

["6",".",".","1","9","5",".",".","."],

[".","9","8",".",".",".",".","6","."],

["8",".",".",".","6",".",".",".","3"],

["4",".",".","8",".","3",".",".","1"],

["7",".",".",".","2",".",".",".","6"],

[".","6",".",".",".",".","2","8","."],

[".",".",".","4","1","9",".",".","5"],

[".",".",".",".","8",".",".","7","9"]]

Output: true

Example 2:

Input: board =
[["8","3",".",".","7",".",".",".","."],

["6",".",".","1","9","5",".",".","."],

[".","9","8",".",".",".",".","6","."],

["8",".",".",".","6",".",".",".","3"],

["4",".",".","8",".","3",".",".","1"],

["7",".",".",".","2",".",".",".","6"],

[".","6",".",".",".",".","2","8","."],

[".",".",".","4","1","9",".",".","5"],

[".",".",".",".","8",".",".","7","9"]]

Output: false

Explanation: Same as Example 1, except with the 5 in the top left corner being modified to 8. Since there are two 8's in the top left 3x3 sub-box, it is invalid.

Constraints:

* board.length == 9
* board[i].length == 9
* board[i][j] is a digit 1-9 or '.'.

#### Answer 9

```javascript
var isValidSudoku = function(board) {
    const colObj = {}
    const rowObj = {}
    const areaArr = new Array(9)

    for (let row = 0; row < 9; row++) {
        for (let col = 0; col < 9; col++) {
            const num = board[row][col]
            if (num === ".") continue
            // row checking
            if (!rowObj[row]) rowObj[row] = new Set()
            if (rowObj[row].has(num)) return false
            else rowObj[row].add(num)

            // col checking
            if (!colObj[col]) colObj[col] = new Set()
            if (colObj[col].has(num)) return false
            else colObj[col].add(num)

            // area checking
            const index = Math.floor(row / 3) * 3 + Math.floor(col / 3)
            if (!areaArr[index]) areaArr[index] = new Set()
            if (areaArr[index].has(num)) return false
            else areaArr[index].add(num)
        }
    }
    return true
};

//Your input
[["5","3",".",".","7",".",".",".","."],["6",".",".","1","9","5",".",".","."],[".","9","8",".",".",".",".","6","."],["8",".",".",".","6",".",".",".","3"],["4",".",".","8",".","3",".",".","1"],["7",".",".",".","2",".",".",".","6"],[".","6",".",".",".",".","2","8","."],[".",".",".","4","1","9",".",".","5"],[".",".",".",".","8",".",".","7","9"]]
//Output
true
//Expected
true
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

#### Answer 10

```javascript
var searchMatrix = function(matrix, target) {
    // initialize a new one dimensional array
    const oneDMatrix = []
    
    // Iterate over the original two dimensional array and add each row to 
    // the new one dimensional array
    for (let i = 0; i < matrix.length; i++) {
        oneDMatrix.push(...matrix[i]);
    }

    // binary search function
    const binarySearch = (arr, target, left, right) => {
        if (left > right) return false;

        const mid = Math.ceil((left + right) / 2);
        if (arr[mid] === target) return true;

        if (target < arr[mid]) {
            return binarySearch(arr, target, left, mid - 1);
        } else if (target > arr[mid]) {
            return binarySearch(arr, target, mid + 1, right);
        }
        return false;
    }

    // return binary search function on the one dimensional array
    return binarySearch(oneDMatrix, target, 0, oneDMatrix.length - 1)
};

//Your input
[[1,3,5,7],[10,11,16,20],[23,30,34,60]]
3
//Output
true
//Expected
true
```

## String

### 387. First Unique Character in a String

Given a string *s*, find the first non-repeating character in it and return its index. If it does not exist, return *-1*.

Example 1:

Input: s = "leetcode"

Output: 0

Example 2:

Input: s = "loveleetcode"

Output: 2

Example 3:

Input: s = "aabb"

Output: -1

Constraints:

* 1 <= s.length <= 10^5
* s consists of only lowercase English letters.

#### Answer 11

```javascript
var firstUniqChar = function (s) {
  const set = new Set();
  for (let i = 0; i < s.length; ++i) {
    if (s.indexOf(s[i], i + 1) === -1 && !set.has(s[i])) return i;
    else set.add(s[i]);
  }
  return -1;
};

//Your input
"leetcode"
//Output
0
//Expected
0
```

### 383. Ransom Note

Given two stings *ransomNote* and *magazine*, return *true* if *ransomNote* can be constructed from *magazine* and *false* otherwise.

Each letter in *magazine* can only be used once in *ransomNote*.

Example 1:

Input: ransomNote = "a", magazine = "b"

Output: false

Example 2:

Input: ransomNote = "aa", magazine = "ab"

Output: false

Example 3:

Input: ransomNote = "aa", magazine = "aab"

Output: true

Constraints:

* 1 <= ransomNote.length, magazine.length <= 10^5
* ransomNote and magazine consist of lowercase English letters.

#### Answer 12

```javascript
var canConstruct = function(ransomNote, magazine) {
    const magazineMap = new Map()
    for (const ch of magazine) {
        magazineMap.set(ch, (magazineMap.get(ch) ?? 0) + 1)
    }
    for (const ch of ransomNote) {
        if (!magazineMap.get(ch))
            return false
        const left = magazineMap.get(ch) - 1
        if (left === 0) 
            magazineMap.delete(ch)
        else
            magazineMap.set(ch, left)
    }
        
    return true
};

//Your input
"a"
"b"
//Output
false
//Expected
false
```

### 242. Valid Anagram

Given two strings *s* and *t*, return *true* if *t* is an anagram of *s*, and *false* otherwise.

Example 1:

Input: s = "anagram", t = "nagaram"

Output: true

Example 2:

Input: s = "rat", t = "car"

Output: false

Constraints:

* 1 <= s.length, t.length <= 5 * 10^4
* s and t consist of lowercase English letters.

Follow up: What if the inputs contain Unicode characters? How would you adapt your solution to such a case?

#### Answer 13

```javascript
var isAnagram = function(s, t) {
  let frequencyCounter1 = {},
    frequencyCounter2 = {}
  
  if(s.length !== t.length) return false

  for (let i of s) {
    frequencyCounter1[i] = (frequencyCounter1[i] || 0) + 1
  }

  for (let i of t) {
    frequencyCounter2[i] = (frequencyCounter2[i] || 0) + 1
  }

  for (let f1 in frequencyCounter1) {
    if (frequencyCounter1[f1] !== frequencyCounter2[f1]) return false
  }

  return true
};

var isAnagram = function(s, t) {
    s = s.split('').sort().join('');
    t = t.split('').sort().join('');

    return s === t;
};
//Your input
"anagram"
"nagaram"
//Output
true
//Expected
true
```

### 141. Linked List Cycle

Given *head*, the head of a linked list, determine if the linked list has a cycle in it.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the *next* pointer. Internally, *pos* is used to denote the index of the node that tail's *next* pointer is connected to. Note that *pos* is not passed as a parameter.

Return true if there is a cycle in the linked list. Otherwise, return false.

Example 1:

![circularlinkedlist](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist.png)

Input: head = [3,2,0,-4], pos = 1

Output: true

Explanation: There is a cycle in the linked list, where the tail connects to the 1st node (0-indexed).

Example 2:

![circularlinkedlist_test2](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test2.png)

Input: head = [1,2], pos = 0

Output: true

Explanation: There is a cycle in the linked list, where the tail connects to the 0th node.

Example 3:

![circularlinkedlist_test3](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test3.png)

Input: head = [1], pos = -1

Output: false

Explanation: There is no cycle in the linked list.

Constraints:

* The number of the nodes in the list is in the range [0, 10^4].
* -10^5 <= Node.val <= 10^5
* pos is -1 or a valid index in the linked-list.

Follow up: Can you solve it using O(1) (i.e. constant) memory?

#### Answer 14

```javascript
var hasCycle = function (head) {
    if (!head) return false;
    let [slow_pointer, fast_pointer] = [head, head];
   
    while (fast_pointer !== null && fast_pointer.next !==null) {
        slow_pointer = slow_pointer.next;
        fast_pointer = fast_pointer.next.next;
        if(slow_pointer === fast_pointer) return true;
    }
    return false
};

const hasCycle = (head) => {
  if (!head) return false;

  let slow = head;
  let fast = head.next;

  while (true) {
    if (!fast || !fast.next) {
      return false;
    }
    if (fast === slow || fast.next === slow) {
      return true;
    }

    slow = slow.next;
    fast = fast.next.next;
  }
};
//Your input
[3,2,0,-4]
1
//Output
true
//Expected
true
```

### 21. Merge Two Sorted Lists

Merge two sorted linked lists and return it as a sorted list. The list should be made by splicing together the nodes of the first two lists.

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

#### Answer 15

```javascript
/*
UNDERSTAND:
-input is given as two linked lists 
-return a sorted list by splicing together the two nodes
l1 = [0, 1, 2, 3]
l2 = [2, 3, 4, 5]
output = [0, 1, 2, 2, 3, 3, 4, 5]

PLAN:
create a helper function to traverse a linked list and push the values into a passed array
sort the array
create a helper function that takes in an array and returns a linked list
return the linked list helper function
*/

function traverseList(list, array) {
    let head = list
    while(head != null) {
        array.push(head.val)
        head = head.next
    }
    
    return array
}

// works backwards last # will be head node
function createList(array) {
    var list = null;
  for (var i = array.length - 1; i >= 0; i--)
    list = {val: array[i], next: list};
  return list;
}

var mergeTwoLists = function(l1, l2) {
    let holder = []
    traverseList(l1, holder)
    traverseList(l2, holder)
    let sortedHolder = holder.sort(function(a, b){return a-b})
    
    return createList(sortedHolder)
};

var mergeTwoLists = function(l1, l2) {
    let current = new ListNode();
    let head = current;
    let headPtr1 = l1, headPtr2 = l2;
   //two head pointer
    while(headPtr1 && headPtr2){
    if(headPtr1.val > headPtr2.val){
        current.next = headPtr2;
        headPtr2 = headPtr2.next;
        current = current.next;
    }else{
       current.next = headPtr1;
        headPtr1 = headPtr1.next;
        current = current.next; 
    }
    }
    if(headPtr1)
        current.next = headPtr1;
    if(headPtr2)
        current.next = headPtr2;
    return head.next;
};

var mergeTwoLists = function(h1, h2) {
    
    if(!h1 && !h2){
        return null;
    }else if(!h1 && h2){
        return h2;
    }else if(h1 && !h2){
        return h1;
    }else if(h1.val < h2.val){
        let cur = h1;
        cur.next = mergeTwoLists(h1.next, h2);
        return cur;
    }else{
        let cur = h2;
        cur.next = mergeTwoLists(h1, h2.next);
        return cur;
    }
};

//Your input
[1,2,4]
[1,3,4]
//Output
[1,1,2,3,4,4]
//Expected
[1,1,2,3,4,4]
```

### 203. Remove Linked List Elements

Given the *head* of a linked list and an integer *val*, remove all the nodes of the linked list that has *Node.val == val*, and return the new head.

Example 1:

![removelinked-list](https://assets.leetcode.com/uploads/2021/03/06/removelinked-list.jpg)

Input: head = [1,2,6,3,4,5,6], val = 6

Output: [1,2,3,4,5]

Example 2:

Input: head = [], val = 1

Output: []

Example 3:

Input: head = [7,7,7,7], val = 7

Output: []

Constraints:

* The number of nodes in the list is in the range [0, 10^4].
* 1 <= Node.val <= 50
* 0 <= val <= 50

#### Answer 16

```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @param {number} val
 * @return {ListNode}

input 
    head of linked list and int
output 
    linked list
constraints
    The number of nodes in the list is in the range [0, 104]. => we can be given an empty linked list/ head
edges
    empty linked list / head

translate
    return a linked list with nodes with input val removed
example1
    [1,2,3,4,5] val = 6 // [1,2,3,4,5]
example2
    [1,1,1,1,1] val = 1 // []
example3
    [1,2,1,2,1,2] val = 2 // [1,1,1]
example4
    [] val = 1 // []
 */
var removeElements = function(head, val) {
// constraint stated: "The number of nodes in the list is in the range [0, 104]. "
// so we have to have a conditional to check if we're given an empty head

  if (!head) {
    return head;
  }
  
  let curr = head;
  
  // loop through curr up until 2nd to last node since our if statement checks the following node
  // we would error out without && curr.next since it will try to do .val on the null node
  while (curr && curr.next) {
    if (curr.next.val === val) {
      curr.next = curr.next.next;
    } else {
      curr = curr.next;
    }
  }
  
  // our loop never checked the head if it was the val to be removed so we use a ternary operator
  // to return the head.next if the current head is to be removed 
  // if not we can return head as is
  return head.val === val ? head.next : head;
};


var removeElements = function(head, val) {
  if(!head) return head
  while(head && head.val == val) head = head.next
  let node = head
  let prv = null
  while(node){
    const next = node.next
    if(node.val === val){
      prv.next = next
    }else{
      prv = node 
    }    
    node = next
  }
  return head
};

//Your input
[1,2,6,3,4,5,6]
6
//Output
[1,2,3,4,5]
//Expected
[1,2,3,4,5]
```

### 206. Reverse Linked List

Given the *head* of a singly linked list, reverse the list, and return the reversed list.

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

#### Answer 17

```javascript
// Recursive Approach
var reverseList = function(head, prev = null) {
    if(!head) return prev;
    let next = head.next;
    head.next = prev;
    return reverseList(next, head);
};

// Iterative Approach
var reverseList = function(head) {
    let [prev, cur] = [null, head]
    while(cur) {
        [cur.next, prev, cur] = [prev, cur, cur.next]
    }
    return prev
};

//Your input
[1,2,3,4,5]
//Output
[5,4,3,2,1]
//Expected
[5,4,3,2,1]
```

### 83. Remove Duplicates from Sorted List

Given the *head* of a sorted linked list, delete all duplicates such that each element appears only once. Return the linked list *sorted* as well.

Example 1:

![list1](https://assets.leetcode.com/uploads/2021/01/04/list1.jpg)

Input: head = [1,1,2]

Output: [1,2]

Example 2:

![list2](https://assets.leetcode.com/uploads/2021/01/04/list2.jpg)

Input: head = [1,1,2,3,3]

Output: [1,2,3]

Constraints:

* The number of nodes in the list is in the range [0, 300].
* -100 <= Node.val <= 100
* The list is guaranteed to be sorted in ascending order.

#### Answer 18

```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @return {ListNode}

input
    linked list
output
    linked list
constraints
    The number of nodes in the list is in the range [0, 300].
    Linked list is sorted (really helpful)
edge
    empty linked list given
 */
var deleteDuplicates = function(head) {
// since our contraint says we can be given an empty linked list we have to do a conditional to check for it
    if (!head) {
      return head;
    }
  
  let curr = head;
  
  /* 
  since the list is sorted in ascending order we'll never have to worry 
  about finding a lesser number later in the list after we've already passed that number
  eg [1,2,3,1] => won't happen
  so we are able to use 1 pointer here since we wont need to reference this val
  after moving onto the next unique val
  we'll always be referencing the current val with our one pointer until the val changes so we dont
  need a second pointer
  */
  
  while (curr && curr.next) {
    if (curr.val === curr.next.val) {
    // checks if next val is a duplicate compared to the current val
    // if it is then we set the current val's next to the following vals next 
    // eg [1,1,2] => [1, x, 2] => [1,2]
      curr.next = curr.next.next;
    } else {
    // if the next val is not the same as the current val then we can 
    // move our pointer to its current next val
      curr = curr.next;
    }
  }
  
  return head;
};


var deleteDuplicates = function(head) {
    let h = head;
    while(h && h.next){
       if(h.val === h.next.val){
           let place = h.next;
           h.next = place.next;
       }else{
        h = h.next;
       }
    }
    return head;
};

//Your input
[1,1,2]
//Output
[1,2]
//Expected
[1,2]
```

## Stack / Queue

### 20. Valid Parentheses

Given a string *s* containing just the characters *'(', ')', '{', '}', '[' and ']'*, determine if the input string is valid.

An input string is valid if:

* Open brackets must be closed by the same type of brackets.
* Open brackets must be closed in the correct order.

Example 1:

Input: s = "()"

Output: true

Example 2:

Input: s = "()[]{}"

Output: true

Example 3:

Input: s = "(]"

Output: false

Example 4:

Input: s = "([)]"

Output: false

Example 5:

Input: s = "{[]}"

Output: true

Constraints:

* 1 <= s.length <= 10^4
* s consists of parentheses only '()[]{}'.

#### Answer 19

```javascript
/*
For loop the input string.

1. if encounter Closing bracket && its corresponding open bracket is on the top of the stack. => stack.pop
2. else cases => stack.push regardless.
3. we return !stack.length
*/
var isValid = function(s) {
    if (s.length % 2 !== 0 ) return false;
    
    var stack = [];
    for (let c of s) {
        if (c === ')' && stack[stack.length -1] === '('){
            stack.pop()
        } else if (c === '}' && stack[stack.length -1] === '{'){
            stack.pop()
        } else if (c === ']' && stack[stack.length -1] === '['){
            stack.pop()
        } else {
            stack.push(c)
        }
        
    }
    
    return !stack.length
};


//Your input
"()"
//Output
true
//Expected
true
```

### 232. Implement Queue using Stacks

Implement a first in first out (FIFO) queue using only two stacks. The implemented queue should support all the functions of a normal queue *(push, peek, pop, and empty)*.

Implement the *MyQueue* class:

* *void push(int x)* Pushes element x to the back of the queue.
* *int pop()* Removes the element from the front of the queue and returns it.
* *int peek()* Returns the element at the front of the queue.
* *boolean empty()* Returns *true* if the queue is empty, *false* otherwise.

Notes:

* You must use only standard operations of a stack, which means only *push to top, peek/pop from top, size, and is empty* operations are valid.
* Depending on your language, the stack may not be supported natively. You may simulate a stack using a list or deque (double-ended queue) as long as you use only a stack's standard operations.

Example 1:

Input

["MyQueue", "push", "push", "peek", "pop", "empty"]

[[], [1], [2], [], [], []]

Output

[null, null, null, 1, 1, false]

Explanation

MyQueue myQueue = new MyQueue();

myQueue.push(1); // queue is: [1]

myQueue.push(2); // queue is: [1, 2] (leftmost is front of the queue)

myQueue.peek(); // return 1

myQueue.pop(); // return 1, queue is [2]

myQueue.empty(); // return false

Constraints:

* 1 <= x <= 9
* At most 100 calls will be made to push, pop, peek, and empty.
* All the calls to pop and peek are valid.

Follow-up: Can you implement the queue such that each operation is amortized O(1) time complexity? In other words, performing n operations will take overall O(n) time even if one of those operations may take longer.

#### Answer 20

```javascript
var MyQueue = function() {
    this.stackOne = [];
    this.stackTwo = [];
    
    this.migrateStack = (canditateStack, targetStack) => {
        while(canditateStack.length) {
            targetStack.push(canditateStack.pop());
        }
        
        return [canditateStack, targetStack];
    }
};

MyQueue.prototype.push = function(x) {
    if(!this.stackTwo.length) {
        this.stackOne.push(x);
        return;
    }
    
    this.migrateStack(this.stackTwo, this.stackOne);
    this.stackOne.push(x);
};

MyQueue.prototype.pop = function() {
    if(!this.stackOne.length) {
        return this.stackTwo.pop();
    }
    
    this.migrateStack(this.stackOne, this.stackTwo);
    return this.stackTwo.pop();
};

MyQueue.prototype.peek = function() {
    if(!this.stackOne.length) {
        return this.stackTwo[this.stackTwo.length - 1];
    }
    
    this.migrateStack(this.stackOne, this.stackTwo);
    return this.stackTwo[this.stackTwo.length - 1];
};

MyQueue.prototype.empty = function() {
    return !this.stackOne.length && !this.stackTwo.length;
};


//Your input
["MyQueue","push","push","peek","pop","empty"]
[[],[1],[2],[],[],[]]
//Output
[null,null,null,1,1,false]
//Expected
[null,null,null,1,1,false]
```

## Tree

### 144. Binary Tree Preorder Traversal

Given the *root* of a binary tree, return the preorder traversal of its nodes' values.

Example 1:

![inorder_1](https://assets.leetcode.com/uploads/2020/09/15/inorder_1.jpg)

Input: root = [1,null,2,3]

Output: [1,2,3]

Example 2:

Input: root = []

Output: []

Example 3:

Input: root = [1]

Output: [1]

Example 4:

![inorder_5](https://assets.leetcode.com/uploads/2020/09/15/inorder_5.jpg)

Input: root = [1,2]

Output: [1,2]

Example 5:

![inorder_4](https://assets.leetcode.com/uploads/2020/09/15/inorder_4.jpg)

Input: root = [1,null,2]

Output: [1,2]

Constraints:

The number of nodes in the tree is in the range [0, 100].
-100 <= Node.val <= 100

Follow up: Recursive solution is trivial, could you do it iteratively?

#### Answer 21

```javascript
var preorderTraversal = function(root) {
    let result = [];
    
    function traversal(root) {
         if(!root) {
            return
          }
        result.push(root.val)
        traversal(root.left);
        traversal(root.right)
     }
    
    traversal(root);
    return result;
   
    
};


//Your input
[1,null,2,3]
//Output
[1,2,3]
//Expected
[1,2,3]
```

### 94. Binary Tree Inorder Traversal

Given the *root* of a binary tree, return the inorder traversal of its nodes' values.

Example 1:

![inorder_1](https://assets.leetcode.com/uploads/2020/09/15/inorder_1.jpg)

Input: root = [1,null,2,3]

Output: [1,3,2]

Example 2:

Input: root = []

Output: []

Example 3:

Input: root = [1]

Output: [1]

Example 4:

![inorder_5](https://assets.leetcode.com/uploads/2020/09/15/inorder_5.jpg)

Input: root = [1,2]

Output: [2,1]

Example 5:

![inorder_4](https://assets.leetcode.com/uploads/2020/09/15/inorder_4.jpg)

Input: root = [1,null,2]

Output: [1,2]

Constraints:

* The number of nodes in the tree is in the range [0, 100].
* -100 <= Node.val <= 100

Follow up: Recursive solution is trivial, could you do it iteratively?

#### Answer 22

```javascript
var inorderTraversal = function(root) {
    if (!root) return []
    return [...inorderTraversal(root.left), root.val, ...inorderTraversal(root.right)]
}


//Your input
[1,null,2,3]
//Output
[1,3,2]
//Expected
[1,3,2]
```

### 145. Binary Tree Postorder Traversal

Given the *root* of a binary tree, return the postorder traversal of its nodes' values.

Example 1:

![pre1](https://assets.leetcode.com/uploads/2020/08/28/pre1.jpg)

Input: root = [1,null,2,3]

Output: [3,2,1]

Example 2:

Input: root = []

Output: []

Example 3:

Input: root = [1]

Output: [1]

Example 4:

![pre3](https://assets.leetcode.com/uploads/2020/08/28/pre3.jpg)

Input: root = [1,2]

Output: [2,1]

Example 5:

![pre2](https://assets.leetcode.com/uploads/2020/08/28/pre2.jpg)

Input: root = [1,null,2]

Output: [2,1]

Constraints:

* The number of the nodes in the tree is in the range [0, 100].
* -100 <= Node.val <= 100

Follow up: Recursive solution is trivial, could you do it iteratively?

#### Answer 23

```javascript
// Stack Solution

var postorderTraversal = function(root) {
    if(!root) return [];

    const stack = [root];
    const result = [];
    while(stack.length > 0) {
        const node = stack.pop();
        result.push(node.val);
        if(node.left) stack.push(node.left);
        if(node.right) stack.push(node.right);
    }
    
    return result.reverse();
};

// Recursive Solution

var postorderTraversal = function(root) {
    const result = [];
    const recursive = (node) => {
        if(!node) return;

        if(node.left) recursive(node.left);
        if(node.right) recursive(node.right);
        result.push(node.val);
    }

    recursive(root);
    return result;
};

//Your input
[1,null,2,3]
//Output
[3,2,1]
//Expected
[3,2,1]
```

### 102. Binary Tree Level Order Traversal

Given the *root* of a binary tree, return the level order traversal of its nodes' values. (i.e., from left to right, level by level).

Example 1:

![tree1](https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg)

Input: root = [3,9,20,null,null,15,7]

Output: [[3],[9,20],[15,7]]

Example 2:

Input: root = [1]

Output: [[1]]

Example 3:

Input: root = []

Output: []

Constraints:

* The number of nodes in the tree is in the range [0, 2000].
* -1000 <= Node.val <= 1000

#### Answer 24

```javascript
var levelOrder = function(root) {  
    let result = [];
    
    if (root === null) return result;
    
    const lot = (root, level) => {
        
        if (!root) return;
        
        if (result[level]) {
            result[level].push(root.val);
        } else {
            result[level] = [root.val];
        }
        lot(root.left, level+1);
        lot(root.right, level+1);
    }
    lot(root, 0)
    
    return result;  
};


var levelOrder = function(root) {
    let q = [root], ans = []
    while (q[0]) {
        let qlen = q.length, row = []
        for (let i = 0; i < qlen; i++) {
            let curr = q.shift()
            row.push(curr.val)
            if (curr.left) q.push(curr.left)
            if (curr.right) q.push(curr.right)
        }
        ans.push(row)            
    }
    return ans
};

//Your input
[3,9,20,null,null,15,7]
//Output
[[3],[9,20],[15,7]]
//Expected
[[3],[9,20],[15,7]]
```

### 104. Maximum Depth of Binary Tree

Given the *root* of a binary tree, return its maximum depth.

A binary tree's *maximum depth* is the number of nodes along the longest path from the root node down to the farthest leaf node.

Example 1:

![tmp-tree](https://assets.leetcode.com/uploads/2020/11/26/tmp-tree.jpg)

Input: root = [3,9,20,null,null,15,7]

Output: 3

Example 2:

Input: root = [1,null,2]

Output: 2

Example 3:

Input: root = []

Output: 0

Example 4:

Input: root = [0]

Output: 1

Constraints:

* The number of nodes in the tree is in the range [0, 10^4].
* -100 <= Node.val <= 100

#### Answer 25

```javascript
var maxDepth = function(root) {
    if(!root) return 0;
    return 1+ Math.max(maxDepth(root.left), maxDepth(root.right)); 
};


var maxDepth = function(root) {
    if(!root) return 0;
    var queue = [root];
    var layers = 0;
    var node = root;
    while(queue.length) {
        var curLevelLen = queue.length;
        for(var i = 0; i < curLevelLen; i++) {
            node = queue.shift();
            if(node.left) queue.push(node.left);
            if(node.right) queue.push(node.right);
        }
        layers++;
    }
    return layers;
};

//Your input
[3,9,20,null,null,15,7]
//Output
3
//Expected
3
```

### 101. Symmetric Tree

Given the root of a binary tree, check whether it is a mirror of itself (i.e., symmetric around its center).

Example 1:

![symtree1](https://assets.leetcode.com/uploads/2021/02/19/symtree1.jpg)

Input: root = [1,2,2,3,4,4,3]

Output: true

Example 2:

![symtree2](https://assets.leetcode.com/uploads/2021/02/19/symtree2.jpg)

Input: root = [1,2,2,null,3,null,3]

Output: false

Constraints:

* The number of nodes in the tree is in the range [1, 1000].
* -100 <= Node.val <= 100

Follow up: Could you solve it both recursively and iteratively?

#### Answer 26

```javascript
// Recursive:

var isSymmetric = function(root) {
    function isEqual(root1, root2) {
        if (!root1 && !root2) return true;
        if (!root1 || !root2) return false;
        return root1.val === root2.val
        && isEqual(root1.left, root2.right)
        && isEqual(root1.right, root2.left);
    }
    if (!root) return true;
    return isEqual(root.left, root.right)
};

// Iterative:

var isSymmetric = function(root) {
    if (!root) return true;
    
    const stack = [root.left, root.right];
    while (stack.length) {
        const currLeft = stack.shift();
        const currRight = stack.shift();
        if (!currLeft && !currRight) continue;
        if ((!currLeft || !currRight) || currLeft.val !== currRight.val) return false;
        stack.push(currLeft.left, currRight.right, currLeft.right, currRight.left);
    }
    return true;
};


//Your input
[1,2,2,3,4,4,3]
//Output
true
//Expected
true
```

### 226. Invert Binary Tree

Given the *root* of a binary tree, invert the tree, and return its root.

Example 1:

![invert1-tree](https://assets.leetcode.com/uploads/2021/03/14/invert1-tree.jpg)

Input: root = [4,2,7,1,3,6,9]

Output: [4,7,2,9,6,3,1]

Example 2:

![invert2-tree](https://assets.leetcode.com/uploads/2021/03/14/invert2-tree.jpg)

Input: root = [2,1,3]

Output: [2,3,1]

Example 3:

Input: root = []

Output: []

Constraints:

* The number of nodes in the tree is in the range [0, 100].
* -100 <= Node.val <= 100

#### Answer 27

```javascript
/*
The strategy is not complicated, and the process of thinking is also directly. So, I'm not going to say too much about it. Just remember, the key point is to swap left child and right child for every node:

* Traverse all nodes
* Swap left child and right child

About traversal, here are 2 common ways - BFS and DFS. Let's try them both.

BFS
The negative for this strategy is it's a little bit complicated to write. But the positive is there's no stack overflow risk.
*/

const invertTree = (node) => node ? ([node.left, node.right] = [invertTree(node.right), invertTree(node.left)], node) : null;

const invertTree = (node) => {
  if (!node) return null;
  [node.left, node.right] = [node.right, node.left];
  invertTree(node.left);
  invertTree(node.right);
  return node;
};

//Your input
[4,2,7,1,3,6,9]
//Output
[4,7,2,9,6,3,1]
//Expected
[4,7,2,9,6,3,1]
```
